
## Boo Signature:
```cs
[DllImport("ntdll.dll", SetLastError : true)]
def NtResumeThread(ThreadHandle as IntPtr, ref SuspendCount as UInt32) as UInt32:
     pass
```
