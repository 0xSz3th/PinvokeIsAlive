
## C# Signature:
```cs
[DllImport("gdiplus.dll", CharSet=CharSet.Unicode, ExactSpelling=true)]
static extern int GdipBitmapSetPixel(HandleRef bitmap, int x, int y, int argb);
```

## VB Signature:
```cs
Declare Function GdipBitmapSetPixel Lib "gdiplus.dll" (TODO) As Int
```

## Alternative Managed API:
```cs
bitmap.SetPixel(int x, int y, Color color);
```
