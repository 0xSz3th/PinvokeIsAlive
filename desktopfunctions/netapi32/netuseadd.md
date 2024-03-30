
## C# Signature:
```cs
using BOOL = System.Boolean;
using DWORD = System.UInt32;
using LPWSTR = System.String;
using NET_API_STATUS = System.UInt32;

[DllImport("NetApi32.dll", SetLastError = true, CharSet = CharSet.Unicode)]
internal static extern NET_API_STATUS NetUseAdd(
     LPWSTR UncServerName,
     DWORD Level,
     ref Structures.USE_INFO_2 Buf,
     out DWORD ParmError);
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
internal struct USE_INFO_2
{
     internal LPWSTR ui2_local;
     internal LPWSTR ui2_remote;
     internal LPWSTR ui2_password;
     internal DWORD  ui2_status;
     internal DWORD  ui2_asg_type;
     internal DWORD  ui2_refcount;
     internal DWORD  ui2_usecount;
     internal LPWSTR ui2_username;
     internal LPWSTR ui2_domainname;
}
```

## Sample Code:
```cs
USE_INFO_2 useInfo    = new USE_INFO_2();
useInfo.ui2_local     = "E:";
useInfo.ui2_remote    = @"\\machine\share";
useInfo.ui2_password  = "password";
useInfo.ui2_asg_type  = 0;    //disk drive
useInfo.ui2_usecount  = 1;
useInfo.ui2_username  = "user";
useInfo.ui2_domainname= "domain"; 

uint paramErrorIndex;
uint returnCode = NetUseAdd(null, 2, ref useInfo, out paramErrorIndex);
if (returnCode != 0)
{
      throw new Win32Exception((int)returnCode);
}
```
