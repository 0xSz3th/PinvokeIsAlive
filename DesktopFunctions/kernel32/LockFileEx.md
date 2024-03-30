
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool LockFileEx(IntPtr hFile, uint dwFlags, uint dwReserved,
   uint nNumberOfBytesToLockLow, uint nNumberOfBytesToLockHigh,
   [In] ref System.Threading.NativeOverlapped lpOverlapped);
```
