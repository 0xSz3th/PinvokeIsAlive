
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool ReadFileScatter(IntPtr hFile, FILE_SEGMENT_ELEMENT []
   aSegementArray, uint nNumberOfBytesToRead, IntPtr lpReserved,
   [In] ref System.Threading.NativeOverlapped lpOverlapped);
```
