
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true)]
static extern IntPtr CreateFileMapping(IntPtr hFile,
   IntPtr lpFileMappingAttributes, PageProtection flProtect, uint dwMaximumSizeHigh,
   uint dwMaximumSizeLow, string lpName);
```
