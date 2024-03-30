
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError=true, CharSet=CharSet.Unicode)]
static extern bool CreateProcessAsUser(
    IntPtr hToken,
    string lpApplicationName,
    string lpCommandLine,
    ref SECURITY_ATTRIBUTES lpProcessAttributes,
    ref SECURITY_ATTRIBUTES lpThreadAttributes,
    bool bInheritHandles,
    uint dwCreationFlags,
    IntPtr lpEnvironment,
    string lpCurrentDirectory,
    ref STARTUPINFO lpStartupInfo,
    out PROCESS_INFORMATION lpProcessInformation);
```

## VB Signature :
```cs
Private Declare Auto Function CreateProcessAsUser Lib "advapi32" ( _
    ByVal hToken As IntPtr, _
    ByVal strApplicationName As String, _
    ByVal strCommandLine As String, _
    ByRef lpProcessAttributes as SECURITY_ATTRIBUTES, _
    ByRef lpThreadAttributes as SECURITY_ATTRIBUTES, _
    ByVal bInheritHandles as Boolean, _
    ByVal dwCreationFlags As Integer, _
    ByVal lpEnvironment As IntPtr, _
    ByVal lpCurrentDriectory As String, _
    ByRef lpStartupInfo As STARTUPINFO, _
    ByRef lpProcessInformation As PROCESS_INFORMATION) As Boolean
```

## VB Signature:
```cs
<DllImport("Advapi32.dll", ExactSpelling:=False, SetLastError:=True, CharSet:=CharSet.Unicode)> _
Private Shared Function CreateProcessAsUser( _
                           ByVal hToken As IntPtr, _
                           ByVal lpApplicationName As String, _
                           <[In](), Out(), [Optional]()> ByVal lpCommandLine As StringBuilder, _
                           ByVal lpProcessAttributes As IntPtr, _
                           ByVal lpThreadAttributes As IntPtr, _
                           <MarshalAs(UnmanagedType.Bool)> ByVal bInheritHandles As Boolean, _
                           ByVal dwCreationFlags As Integer, _
                           ByVal lpEnvironment As IntPtr, _
                           ByVal lpCurrentDirectory As String, _
                           <[In]()> ByRef lpStartupInfo As StartupInfo, _
                           <Out()> ByRef lpProcessInformation As PROCESS_INFORMATION) As <MarshalAs(UnmanagedType.Bool)> Boolean
End Function
```

## C# Sample Code:
```cs
// Declare variables
PROCESS_INFORMATION pi;
STARTUPINFO si;
System.IntPtr hToken;

// Initialize structs
si.cb = Marshal.SizeOf(si);

// Get the user token
if (LogonUser(userPart, domainPart, password, LOGON_TYPE.LOGON32_LOGON_BATCH, LOGON_PROVIDER.LOGON32_PROVIDER_DEFAULT, hToken))
{
     // Create structs
     SECURITY_ATTRIBUTES saProcessAttributes = new SECURITY_ATTRIBUTES();
     SECURITY_ATTRIBUTES saThreadAttributes = new SECURITY_ATTRIBUTES();     

     // Now create the process as the user
     if (!CreateProcessAsUser(hToken, String.Empty, commandLine,
     null, saThreadAttributes, false, 0, IntPtr.Zero, 0, si, pi))
     {
     // Throw exception
     throw new Exception("Failed to CreateProcessAsUser");
     }
}
```

## VB Sample Code:
```cs
Dim pi As PROCESS_INFORMATION
Dim si As STARTUPINFO
si.cb = Marshal.SizeOf(si)
Dim hToken as System.IntPtr 
If LogonUser(userPart, domainPart, password, LOGON_TYPE.LOGON32_LOGON_BATCH, _
          LOGON_PROVIDER.LOGON32_PROVIDER_DEFAULT, hToken) Then

     Dim saProcessAttributes as SECURITY_ATTRIBUTES = new SECURITY_ATTRIBUTES 
     Dim saThreadAttributes as SECURITY_ATTRIBUTES = new SECURITY_ATTRIBUTES  
     If Not CreateProcessAsUser(hToken, "", strCmdLine, Nothing, _
     saThreadAttributes, False, 0, IntPtr.Zero, 0, si, pi) Then

     Throw New Exception(Err.Description)
     End If
End If
```
