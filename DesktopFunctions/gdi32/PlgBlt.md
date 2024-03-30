
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern bool PlgBlt(IntPtr hdcDest, POINT [] lpPoint, IntPtr hdcSrc,
   int nXSrc, int nYSrc, int nWidth, int nHeight, IntPtr hbmMask, int xMask,
   int yMask);
```
