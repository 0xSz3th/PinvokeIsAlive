
## C# Signature:
```cs
[DllImport("Advapi32.dll", SetLastError=true, EntryPoint="CredWriteW", CharSet=CharSet.Unicode)]
static extern bool CredWrite([In] ref Credential userCredential, [In] UInt32 flags);
```

## VB Signature:
```cs
Declare Function CredWriteW Lib "advapi32.dll" ( _
  ByRef crede As Credential, _
  ByVal flags As UInteger _
) As Boolean
```

## VB.NET type:
```cs
<Runtime.InteropServices.StructLayout(Runtime.InteropServices.LayoutKind.Sequential, CharSet:=Runtime.InteropServices.CharSet.Unicode)> _
Structure Credential
   Dim Flags As UInteger
   Dim Type As UInteger
   Dim TargetName$
   Dim Comment$
   Dim LastWritten As System.Runtime.InteropServices.ComTypes.FILETIME
   Dim CredentialBlobSize As UInteger
   Dim CredentialBlob As IntPtr
   Dim Persist As UInteger
   Dim AttributeCount As UInteger
   Dim Attributes As IntPtr
   Dim TargetAlias$
   Dim UserName$
End Structure
```

## User-Defined Types:
```cs
enum CRED_TYPE : uint
{
     CRED_TYPE_GENERIC = 1,
     CRED_TYPE_DOMAIN_PASSWORD = 2,
     CRED_TYPE_DOMAIN_CERTIFICATE = 3,
     CRED_TYPE_DOMAIN_VISIBLE_PASSWORD = 4
}

enum CRED_PERSIST : uint
{
     CRED_PERSIST_SESSION = 1,
     CRED_PERSIST_LOCAL_MACHINE = 2,

     CRED_PERSIST_ENTERPRISE = 3
}

[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Unicode)]
private struct Credential
{
     public UInt32 flags;
     public UInt32 type;
     public string targetName;
     public string comment;
     //public System.Runtime.InteropServices.FILETIME lastWritten; // .NET 1.1
     public System.Runtime.InteropServices.ComTypes.FILETIME lastWritten; // .NET 2.0
     public UInt32 credentialBlobSize;
     public IntPtr credentialBlob;
     public UInt32 persist;
     public UInt32 attributeCount;
     public IntPtr credAttribute;
     public string targetAlias;
     public string userName;
}
```

## Notes:
```cs
http://blogs.msdn.com/peerchan/pages/487834.aspx
```

## Sample Code:
```cs
Dim cred As New Credential
Dim strKey$ = "a3b9236"

With cred
  .Flags = 0
  .Type = &H1
  .TargetName = "API_key"
  .Comment = String.Empty
  .CredentialBlobSize = CType(Text.Encoding.Unicode.GetBytes(strKey).Length, UInteger)
  .CredentialBlob = Runtime.InteropServices.Marshal.StringToCoTaskMemUni(strKey)
  .Persist = &H2
  .AttributeCount = 0
  .Attributes = IntPtr.Zero
  .TargetAlias = String.Empty
  .UserName = String.Empty
End With

If CredWriteW(cred, 0) <> True Then
  a = New System.ComponentModel.Win32Exception()
  Console.WriteLine(a.Message)
End If
```

## Sample Code:
```cs
internal static void AddDomainUserCredential(string target, string userName, string password)
{
     Credential userCredential = new Credential();

     userCredential.targetName = target;
     userCredential.type = (UInt32)CRED_TYPE.CRED_TYPE_DOMAIN_PASSWORD;
     userCredential.userName = userName;
     userCredential.attributeCount = 0;
     userCredential.persist = (UInt32)CRED_PERSIST.CRED_PERSIST_ENTERPRISE;
     byte[] bpassword = Encoding.Unicode.GetBytes(password);
     userCredential.credentialBlobSize = (UInt32)bpassword.Length;
     userCredential.credentialBlob = Marshal.StringToCoTaskMemUni(password);
     if (!Unmanaged.CredWrite(ref userCredential, 0))
     {
     throw new System.ComponentModel.Win32Exception(Marshal.GetLastWin32Error());
     }
}
```

## Sample Code:
```cs
$sig = @"
[DllImport("Advapi32.dll", SetLastError=true, EntryPoint="CredWriteW", CharSet=CharSet.Unicode)]
public static extern bool CredWrite([In] ref Credential userCredential, [In] UInt32 flags);

[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Unicode)]
public struct Credential
{
     public UInt32 flags;
     public UInt32 type;
     public IntPtr targetName;
     public IntPtr comment;
     public System.Runtime.InteropServices.ComTypes.FILETIME lastWritten;
     public UInt32 credentialBlobSize;
     public IntPtr credentialBlob;
     public UInt32 persist;
     public UInt32 attributeCount;
     public IntPtr Attributes;
     public IntPtr targetAlias;
     public IntPtr userName;
}
"@
Add-Type -MemberDefinition $sig -Namespace "ADVAPI32" -Name 'Util'

$cred = New-Object ADVAPI32.Util+Credential
$cred.flags = 0
$cred.type = 2
$cred.targetName = [System.Runtime.InteropServices.Marshal]::StringToCoTaskMemUni('server1')
$cred.userName = [System.Runtime.InteropServices.Marshal]::StringToCoTaskMemUni('domain\user')
$cred.attributeCount = 0
$cred.persist = 2
$password = "password"
$cred.credentialBlobSize = [System.Text.Encoding]::Unicode.GetBytes($password).length
$cred.credentialBlob = [System.Runtime.InteropServices.Marshal]::StringToCoTaskMemUni($password)
[ADVAPI32.Util]::CredWrite([ref]$cred,0)
```
