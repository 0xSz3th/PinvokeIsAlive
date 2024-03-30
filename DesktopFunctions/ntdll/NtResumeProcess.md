
## C# Signature:
```cs
[DllImport("ntdll.dll", PreserveSig = false, SetLastError = true)]
public static extern void NtResumeProcess(IntPtr processHandle);
```

## VB Signature:
```cs
<DllImport("ntdll.dll", PreserveSig:=False, SetLastError:=True)> _
    Public Shared Sub NtResumeProcess(ByVal ProcessHandle As IntPtr)
    End Sub
```
