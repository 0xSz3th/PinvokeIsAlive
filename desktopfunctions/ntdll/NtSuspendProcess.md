
## C# Signature:
```cs
[DllImport("ntdll.dll", PreserveSig = false)]
public static extern void NtSuspendProcess(IntPtr processHandle);
```

## VB Signature:
```cs
<DllImport("ntdll.dll", PreserveSig:=False)> _
    Public Shared Sub NtSuspendProcess(ByVal ProcessHandle As IntPtr)
    End Sub
```
