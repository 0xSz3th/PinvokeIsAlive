
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern IntPtr MapViewOfFileEx(IntPtr hFileMappingObject,
   FileMapAccessType dwDesiredAccess, uint dwFileOffsetHigh, uint dwFileOffsetLow,
   UIntPtr dwNumberOfBytesToMap, IntPtr lpBaseAddress);
```
