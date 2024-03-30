
## Boo Signature:
```cs
[DllImport("ntdll.dll", SetLastError : true)]
def NtSetContextThread(ThreadHandle as IntPtr, ref lpContext as Context) as UInt32:
     pass

[DllImport("ntdll.dll", SetLastError : true)]
def NtSetContextThread(ThreadHandle as IntPtr, lpContext as IntPtr) as UInt32:
     pass
```
