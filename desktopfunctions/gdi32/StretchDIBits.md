
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern int StretchDIBits(IntPtr hdc, int XDest, int YDest,
   int nDestWidth, int nDestHeight, int XSrc, int YSrc, int nSrcWidth,
   int nSrcHeight, byte [] lpBits, [In] ref BITMAPINFO lpBitsInfo, uint iUsage,
   uint dwRop);
```
