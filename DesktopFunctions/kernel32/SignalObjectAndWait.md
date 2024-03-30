
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern uint SignalObjectAndWait(IntPtr hObjectToSignal,
   IntPtr hObjectToWaitOn, uint dwMilliseconds, bool bAlertable);
```
