# QueueUserAPC

\[DllImport("kernel32.dll")]     public static extern IntPtr QueueUserAPC(IntPtr pfnAPC, IntPtr hThread, IntPtr dwData);

### Boo Signature:

```cs
[DllImport("kernel32.dll", SetLastError : true)]
def QueueUserAPC(pfnAPC as IntPtr, hThread as IntPtr, dwData as UInt32) as UInt32:
     pass
```
