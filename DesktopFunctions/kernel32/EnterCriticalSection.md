
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern void EnterCriticalSection(ref CRITICAL_SECTION
   lpCriticalSection);
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct CRITICAL_SECTION
{
    public IntPtr DebugInfo;
    public int LockCount;
    public int RecursionCount;
    public IntPtr OwningThread;
    public IntPtr LockSemaphore;
    public UIntPtr SpinCount;
}
```
