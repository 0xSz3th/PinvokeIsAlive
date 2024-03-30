
## C# Signature:
```cs
[DllImport("Kernel32.dll", SetLastError = true, ExactSpelling = true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool CheckRemoteDebuggerPresent(SafeHandle hProcess, [MarshalAs(UnmanagedType.Bool)]ref bool isDebuggerPresent);
```

## VB Signature:
```cs
Declare Function CheckRemoteDebuggerPresent Lib "kernel32.dll"
(ByVal hProcess As Long, ByVal fResult As Boolean) As Boolean
```

## Boo Signature:
```cs
[DllImport("kernel32.dll", SetLastError : true)]
def CheckRemoteDebuggerPresent(hProcess as IntPtr, ref DebuggerPresent as bool) as bool:
     pass
```

## Sample Code:
```cs
'For VB.NET
Public Class Form1
    Declare Function CheckRemoteDebuggerPresent Lib "kernel32.dll" _  
    (ByVal hProcess As Long, ByVal fResult As Boolean) As Boolean
        Dim bool As Boolean
        Dim proc As Process = Process.GetCurrentProcess()

    Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load
            Debug.Print(CStr(CheckRemoteDebuggerPresent(proc.Handle, bool)))
    End Sub
End Class
```
