
## C# Signature:
```cs
[DllImport("gdiplus.dll", SetLastError=true)]
static extern int GdipCreateBitmapFromGdiDib(IntPtr bminfo, IntPtr pixdat, ref IntPtr image);
```

## VB Signature:
```cs
Declare Function GdipCreateBitmapFromGdiDib Lib "GdiPlus.dll" (ByRef GdiBitmapInfo As BITMAPINFO, ByVal GdiBitmapData As Long, ByRef bitmap As Long) As Status
```

## Sample Code:
```cs
IntPtr img = IntPtr.Zero;
    Guid clsid;

    if(!GetCodecClsid(filename, out clsid))
    {
        return false;
    }

    int st = GdipCreateBitmapFromGdiDib(bminfo, pixdat, ref img);

    if((st != 0) || (img == IntPtr.Zero))
    {
        return false;
    }

    st = GdipSaveImageToFile(img, filename, ref clsid, IntPtr.Zero);
    GdipDisposeImage(img);
    return st == 0;
```
