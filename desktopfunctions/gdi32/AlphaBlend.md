
## C# Signature:
```cs
[DllImport("gdi32.dll", EntryPoint="GdiAlphaBlend")]
public static extern bool AlphaBlend(IntPtr hdcDest, int nXOriginDest, int nYOriginDest,
    int nWidthDest, int nHeightDest,
    IntPtr hdcSrc, int nXOriginSrc, int nYOriginSrc, int nWidthSrc, int nHeightSrc,
    BLENDFUNCTION blendFunction);
```

## VB Signature:
```cs
Public Declare Function AlphaBlend Lib "gdi32.dll" Alias "GdiAlphaBlend" 
    (ByVal hdcDest As IntPtr, ByVal nXOriginDest As Integer, ByVal nYOriginDest As Integer, 
    ByVal nWidthDest As Integer, ByVal nHeightDest As Integer, 
    ByVal hdcSrc As IntPtr, ByVal nXOriginSrc As Integer, ByVal nYOriginSrc As Integer, 
    ByVal nWidthSrc As Integer, ByVal nHeightSrc As Integer, 
    ByVal blendFunction As BLENDFUNCTION) As Boolean
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct BLENDFUNCTION
{
    byte BlendOp;
    byte BlendFlags;
    byte SourceConstantAlpha;
    byte AlphaFormat;

    public BLENDFUNCTION(byte op, byte flags, byte alpha, byte format)
    {
    BlendOp = op;
    BlendFlags = flags;
    SourceConstantAlpha = alpha;
    AlphaFormat = format;
    }
}

//
// currently defined blend operation
//
const int AC_SRC_OVER = 0x00;

//
// currently defined alpha format
//
const int AC_SRC_ALPHA = 0x01;
```

## Sample Code:
```cs
[DllImport("gdi32.dll", EntryPoint = "GdiAlphaBlend")]
public static extern bool AlphaBlend(IntPtr hdcDest, int nXOriginDest, int nYOriginDest,
   int nWidthDest, int nHeightDest,
   IntPtr hdcSrc, int nXOriginSrc, int nYOriginSrc, int nWidthSrc, int nHeightSrc,
   BLENDFUNCTION blendFunction);

[DllImport("gdi32.dll")]
public static extern bool BitBlt(IntPtr hObject, int nXDest, int nYDest, int nWidth,
   int nHeight, IntPtr hObjSource, int nXSrc, int nYSrc,  TernaryRasterOperations dwRop);    

[DllImport("gdi32.dll", ExactSpelling=true, SetLastError=true)]
static extern IntPtr CreateCompatibleDC(IntPtr hdc);

[DllImport("gdi32.dll", ExactSpelling=true, SetLastError=true)]
static extern bool DeleteDC(IntPtr hdc);

[DllImport("gdi32.dll", ExactSpelling=true, SetLastError=true)]
static extern IntPtr SelectObject(IntPtr hdc, IntPtr hgdiobj);

[DllImport("gdi32.dll", ExactSpelling=true, SetLastError=true)]
static extern bool DeleteObject(IntPtr hObject);

[StructLayout(LayoutKind.Sequential)]
public struct BLENDFUNCTION
{
   byte BlendOp;
   byte BlendFlags;
   byte SourceConstantAlpha;
   byte AlphaFormat;

   public BLENDFUNCTION(byte op, byte flags, byte alpha, byte format)
   {
     BlendOp = op;
     BlendFlags = flags;
     SourceConstantAlpha = alpha;
     AlphaFormat = format;
   }
}

const byte AC_SRC_OVER = 0x00;
const byte AC_SRC_ALPHA = 0x01;

protected override void OnPaint(PaintEventArgs e) {
    IntPtr pTarget = e.Graphics.GetHdc();
    IntPtr pSource = CreateCompatibleDC(pTarget);
    IntPtr pOrig = SelectObject(pSource, bmp.GetHbitmap(Color.Black));
    AlphaBlend(pTarget, 0, 0, bmp.Width, bmp.Height, pSource, 0, 0, bmp.Width, bmp.Height, new BLENDFUNCTION(AC_SRC_OVER, 0, 0xff, AC_SRC_ALPHA));
    IntPtr pNew = SelectObject(pSource, pOrig);
    DeleteObject(pNew);
    DeleteDC(pSource);
    e.Graphics.ReleaseHdc(pTarget);
}
```
