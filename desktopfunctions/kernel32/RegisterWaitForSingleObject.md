
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool RegisterWaitForSingleObject(out IntPtr phNewWaitObject,
   IntPtr hObject, WaitOrTimerDelegate Callback, IntPtr Context,
   uint dwMilliseconds, uint dwFlags);
```
