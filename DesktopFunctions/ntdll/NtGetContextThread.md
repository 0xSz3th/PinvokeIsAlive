
## C# Signature:
```cs
[DllImport("ntdll.dll", SetLastError=true)]
static extern TODO NtGetContextThread(TODO);
```

## VB Signature:
```cs
<DllImport("ntdll")> Private Shared Function NtGetContextThread(ByVal hThr As IntPtr, ByVal CNTXT As UInteger()) As <MarshalAs(UnmanagedType.Bool)> Boolean
```

## Boo Signature:
```cs
[DllImport("ntdll.dll", SetLastError : true)]
def NtGetContextThread(ThreadHandle as IntPtr, ref lpContext as Context) as UInt32:
     pass

[DllImport("ntdll.dll", SetLastError : true)]
def NtGetContextThread(ThreadHandle as IntPtr, lpContext as IntPtr) as UInt32:
     pass
```
