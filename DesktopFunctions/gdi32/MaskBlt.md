
## C# Signature:
```cs
[DllImport("gdi32.dll", SetLastError=true)]
static extern bool MaskBlt(
  IntPtr     hdcDest,
  int     xDest,
  int     yDest,
  int     width,
  int     height,
  IntPtr     hdcSrc,
  int     xSrc,
  int     ySrc,
  IntPtr hbmMask,
  int     xMask,
  int     yMask,
  uint   rop);
```

## VB Signature:
```cs
Declare Function MaskBlt Lib "gdi32.dll" (TODO) As TODO
```
