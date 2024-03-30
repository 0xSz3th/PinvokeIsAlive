
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern int SetDIBitsToDevice(IntPtr hdc, int XDest, int YDest, uint
   dwWidth, uint dwHeight, int XSrc, int YSrc, uint uStartScan, uint cScanLines,
   byte [] lpvBits, [In] ref BITMAPINFO lpbmi, uint fuColorUse);
```
