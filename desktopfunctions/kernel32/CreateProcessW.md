
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true, CharSet = CharSet.Ansi)]
static extern bool CreateProcess(string lpApplicationName, string lpCommandLine,
IntPtr lpProcessAttributes, IntPtr lpThreadAttributes, bool bInheritHandles,
uint dwCreationFlags, IntPtr lpEnvironment, string lpCurrentDirectory,
[In] ref STARTUPINFO lpStartupInfo, out PROCESS_INFORMATION
lpProcessInformation);
```

## VB Signature:
```cs
Declare Function CreateProcessW Lib "kernel32.dll" (TODO) As TODO
```
