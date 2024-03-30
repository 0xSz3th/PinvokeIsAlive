
## C# Definition:
```cs
[DllImport("advapi32", SetLastError = true, CharSet = CharSet.Unicode)]
public static extern bool CreateProcessWithTokenW(IntPtr hToken, LogonFlags dwLogonFlags, string lpApplicationName, string lpCommandLine, CreationFlags dwCreationFlags, IntPtr lpEnvironment, string lpCurrentDirectory, [In] ref STARTUPINFO lpStartupInfo, out PROCESS_INFORMATION lpProcessInformation);
```

## C# Definition:
```cs
[DllImport("advapi32", SetLastError = true, CharSet = CharSet.Unicode)]
    public static extern bool CreateProcessWithTokenW(
        IntPtr hToken, 
        UInt32 dwLogonFlags, 
        string lpApplicationName, 
        string lpCommandLine, 
        UInt32 dwCreationFlags, 
        IntPtr lpEnvironment, 
        string lpCurrentDirectory, 
        [In] ref STARTUPINFO lpStartupInfo, 
        out PROCESS_INFORMATION lpProcessInformation);
```

## C# Definition:
```cs
public struct PROCESS_INFORMATION
    {
    public IntPtr hProcess;
    public IntPtr hThread;
    public int dwProcessId;
    public int dwThreadId;
    }

    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
    public struct STARTUPINFO
    {
    public Int32 cb;
    public string lpReserved;
    public string lpDesktop;
    public string lpTitle;
    public Int32 dwX;
    public Int32 dwY;
    public Int32 dwXSize;
    public Int32 dwYSize;
    public Int32 dwXCountChars;
    public Int32 dwYCountChars;
    public Int32 dwFillAttribute;
    public Int32 dwFlags;
    public Int16 wShowWindow;
    public Int16 cbReserved2;
    public IntPtr lpReserved2;
    public IntPtr hStdInput;
    public IntPtr hStdOutput;
    public IntPtr hStdError;
    }
```

## VB Definition:
```cs
Public Shared Function CreateProcessWithTokenW(hToken As IntPtr, dwLogonFlags As Integer, lpApplicationName As String, lpCommandLine As String, dwCreationFlags As Integer, lpEnvironment As IntPtr, lpCurrentDirectory As IntPtr, ByRef lpStartupInfo As STARTUPINFO, ByRef lpProcessInformation As PROCESS_INFORMATION) As Boolean
    End Function
```

## User-Defined Field Types:
```cs
public enum LogonFlags
{
     /// <summary>
     /// Log on, then load the user's profile in the HKEY_USERS registry key. The function
     /// returns after the profile has been loaded. Loading the profile can be time-consuming,
     /// so it is best to use this value only if you must access the information in the 
     /// HKEY_CURRENT_USER registry key. 
     /// NOTE: Windows Server 2003: The profile is unloaded after the new process has been
     /// terminated, regardless of whether it has created child processes.
     /// </summary>
     /// <remarks>See LOGON_WITH_PROFILE</remarks>
     WithProfile = 1,
     /// <summary>
     /// Log on, but use the specified credentials on the network only. The new process uses the
     /// same token as the caller, but the system creates a new logon session within LSA, and
     /// the process uses the specified credentials as the default credentials.
     /// This value can be used to create a process that uses a different set of credentials
     /// locally than it does remotely. This is useful in inter-domain scenarios where there is
     /// no trust relationship.
     /// The system does not validate the specified credentials. Therefore, the process can start,
     /// but it may not have access to network resources.
     /// </summary>
     /// <remarks>See LOGON_NETCREDENTIALS_ONLY</remarks>
     NetCredentialsOnly
```

## User-Defined Field Types:
```cs
DefaultErrorMode = 0x04000000,
    NewConsole = 0x00000010,
    NewProcessGroup = 0x00000200,
    SeparateWOWVDM = 0x00000800,
    Suspended = 0x00000004,
    UnicodeEnvironment = 0x00000400,
    ExtendedStartupInfoPresent = 0x00080000
```
