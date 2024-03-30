
## C# Signature:
```cs
[DllImport("Secur32.dll", SetLastError = false)]
private static extern NtStatus LsaEnumerateLogonSessions(out uint LogonSessionCount, out IntPtr LogonSessionList);
```

## VB Signature:
```cs
Declare Function LsaEnumerateLogonSessions Lib "secur32.dll" (TODO) As TODO
```

## Sample Code:
```cs
Clear-Host
  $TypeDefinition=@'
  using System;
  namespace LogonNameSpace {
      using System;
      using System.Runtime.InteropServices;

      public enum SECURITY_LOGON_TYPE : uint {
      Interactive = 2,    //The security principal is logging on interactively.
      Network,        //The security principal is logging using a network.
      Batch,          //The logon is for a batch process.
      Service,        //The logon is for a service account.
      Proxy,          //Not supported.
      Unlock,         //The logon is an attempt to unlock a workstation.
      NetworkCleartext,       //The logon is a network logon with cleartext credentials.
      NewCredentials,     //Allows the caller to clone its current token and specify new credentials for outbound connections.
      RemoteInteractive,      //A terminal server session that is both remote and interactive.
      CachedInteractive,      //Attempt to use the cached credentials without going out across the network.
      CachedRemoteInteractive,// Same as RemoteInteractive, except used internally for auditing purposes.
      CachedUnlock        // The logon is an attempt to unlock a workstation.
      }

      [StructLayout(LayoutKind.Sequential)]
      public struct LSA_UNICODE_STRING {
      public UInt16 Length;
      public UInt16 MaximumLength;
      public IntPtr buffer;
      }

      [StructLayout(LayoutKind.Sequential)]
      public struct LUID {
      public UInt32 LowPart;
      public UInt32 HighPart;
      }

      [StructLayout(LayoutKind.Sequential)]
      public struct SECURITY_LOGON_SESSION_DATA {
      public UInt32 Size;
      public LUID LoginID;
      public LSA_UNICODE_STRING Username;
      public LSA_UNICODE_STRING LoginDomain;
      public LSA_UNICODE_STRING AuthenticationPackage;
      public UInt32 LogonType;
      public UInt32 Session;
      public IntPtr PSiD;
      public UInt64 LoginTime;
      public LSA_UNICODE_STRING LogonServer;
      public LSA_UNICODE_STRING DnsDomainName;
      public LSA_UNICODE_STRING Upn;
      }

      public sealed class LogonClass {
      [DllImport("secur32.dll", SetLastError = false)]
      public static extern uint LsaFreeReturnBuffer(IntPtr buffer);

      [DllImport("Secur32.dll", SetLastError = false)]
      public static extern uint LsaEnumerateLogonSessions(out UInt64 LogonSessionCount, out IntPtr LogonSessionList);

      [DllImport("Secur32.dll", SetLastError = false)]
      public static extern uint LsaGetLogonSessionData(IntPtr luid, out IntPtr ppLogonSessionData);
      }
  }
  '@
  Add-Type -TypeDefinition $TypeDefinition > $null

  $count=[System.UInt64]0
  $luidPtr=[System.IntPtr]::Zero
  # Gets an array of pointers to LUIDs
  [LogonNameSpace.LogonClass]::LsaEnumerateLogonSessions([ref]$count, [ref]$luidPtr) > $null
  # Set the pointer to the start of the array
  $iter=$luidPtr                     
  $Results=@()
  for ($i=0; $i -lt $count; $i++) {
    $sessionData=[System.IntPtr]::new(0)
    [LogonNameSpace.LogonClass]::LsaGetLogonSessionData($iter, [ref]$sessionData) > $null

    $data=[System.Runtime.InteropServices.Marshal]::PtrToStructure($sessionData,[System.Type][LogonNameSpace.SECURITY_LOGON_SESSION_DATA])

    # if we have a valid logon
    if ($data.PSiD -ne [System.IntPtr]::Zero) {
      $secType=New-Object LogonNameSpace.SECURITY_LOGON_TYPE
      $secType.value__=$data.LogonType
      $Result=New-Object -Type PSObject -Property @{UserName=[System.Runtime.InteropServices.Marshal]::PtrToStringUni($data.Username.buffer).Trim();
                            Domain=[System.Runtime.InteropServices.Marshal]::PtrToStringUni($data.LoginDomain.buffer).Trim()
                            Auth=[System.Runtime.InteropServices.Marshal]::PtrToStringUni($data.AuthenticationPackage.buffer).Trim()
                            LogonType=$secType;
                            LogonTime=[System.DateTime]::new($data.LoginTime);
                            SessionID=$data.Session;
                            SID=[System.Security.Principal.SecurityIdentifier]::new($data.PSiD)}
      $Results+=$Result
      # move the pointer forward
      $iter=[System.IntPtr]::Add($iter,[System.Runtime.InteropServices.Marshal]::SizeOf([System.Type][LogonNameSpace.LUID]))

      # free the SECURITY_LOGON_SESSION_DATA memory in the struct
      [LogonNameSpace.LogonClass]::LsaFreeReturnBuffer($sessionData) > $null
    }
  }
  # free the array of LUIDs
  [LogonNameSpace.LogonClass]::LsaFreeReturnBuffer($luidPtr) > $null

  $Results | Sort-Object -Property UserName | Format-Table -Property UserName,Domain,Auth,LogonType,LogonTime,SessionID
```
