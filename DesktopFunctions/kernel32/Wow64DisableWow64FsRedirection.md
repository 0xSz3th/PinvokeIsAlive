
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true)]
public static extern bool Wow64DisableWow64FsRedirection(ref IntPtr ptr);
```

## VB Signature:
```cs
Declare Function Wow64DisableWow64FsRedirection Lib "kernel32.dll" (ByRef ptr As IntPtr) As Boolean
```

## Sample Code:
```cs
string windir = Environment.ExpandEnvironmentVariables("%windir%");
        string system32dir = Path.Combine(windir, "System32");
        string serverManagementCmd = Path.Combine(system32dir, "ServerManagerCmd.exe");
        bool isServerManagerCmdFound = File.Exists(serverManagementCmd);
        Debug.WriteLine("Is ServerManagerCmd.exe accessible:\t" + isServerManagerCmdFound.ToString());
        IntPtr ptr = new IntPtr();
        bool isWow64FsRedirectionDisabled = Wow64DisableWow64FsRedirection(ref ptr);
        Debug.WriteLine("Is Wow64Fs Redirection disabled:\t" + isWow64FsRedirectionDisabled);
        if (isWow64FsRedirectionDisabled)
        {
        isServerManagerCmdFound = File.Exists(serverManagementCmd);
        Debug.WriteLine("Is ServerManagerCmd.exe accessible:\t" + isServerManagerCmdFound.ToString());
        bool isWow64FsRedirectionReverted = Wow64RevertWow64FsRedirection(ptr);
        Debug.WriteLine("Is Wow64Fs Redirection reverted:\t" + isWow64FsRedirectionReverted);
        }
```
