
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool CreatePipe(out IntPtr hReadPipe, out IntPtr hWritePipe,
   ref SECURITY_ATTRIBUTES lpPipeAttributes, uint nSize);
```

## VB Definition:
```cs
Function CreatePipe Lib "kernel32" (phReadPipe As Long, phWritePipe As Long, lpPipeAttributes As Any, ByVal nSize As Long) As Long
```
