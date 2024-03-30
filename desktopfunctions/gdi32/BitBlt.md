
## C# Signature:
```cs
/// <summary>
///    Performs a bit-block transfer of the color data corresponding to a
///    rectangle of pixels from the specified source device context into
///    a destination device context.
/// </summary>
/// <param name="hdc">Handle to the destination device context.</param>
/// <param name="nXDest">The leftmost x-coordinate of the destination rectangle (in pixels).</param>
/// <param name="nYDest">The topmost y-coordinate of the destination rectangle (in pixels).</param>
/// <param name="nWidth">The width of the source and destination rectangles (in pixels).</param>
/// <param name="nHeight">The height of the source and the destination rectangles (in pixels).</param>
/// <param name="hdcSrc">Handle to the source device context.</param>
/// <param name="nXSrc">The leftmost x-coordinate of the source rectangle (in pixels).</param>
/// <param name="nYSrc">The topmost y-coordinate of the source rectangle (in pixels).</param>
/// <param name="dwRop">A raster-operation code.</param>
/// <returns>
///    <c>true</c> if the operation succeedes, <c>false</c> otherwise. To get extended error information, call <see cref="System.Runtime.InteropServices.Marshal.GetLastWin32Error"/>.
/// </returns>
[DllImport("gdi32.dll", EntryPoint = "BitBlt", SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool BitBlt([In] IntPtr hdc, int nXDest, int nYDest, int nWidth, int nHeight, [In] IntPtr hdcSrc, int nXSrc, int nYSrc, TernaryRasterOperations dwRop);
```

## VB.NET Signature:
```cs
''' <summary>
'''    Performs a bit-block transfer of the color data corresponding to a
'''    rectangle of pixels from the specified source device context into
'''    a destination device context.
''' </summary>
''' <param name="hdc">Handle to the destination device context.</param>
''' <param name="nXDest">The leftmost x-coordinate of the destination rectangle (in pixels).</param>
''' <param name="nYDest">The topmost y-coordinate of the destination rectangle (in pixels).</param>
''' <param name="nWidth">The width of the source and destination rectangles (in pixels).</param>
''' <param name="nHeight">The height of the source and the destination rectangles (in pixels).</param>
''' <param name="hdcSrc">Handle to the source device context.</param>
''' <param name="nXSrc">The leftmost x-coordinate of the source rectangle (in pixels).</param>
''' <param name="nYSrc">The topmost y-coordinate of the source rectangle (in pixels).</param>
''' <param name="dwRop">A raster-operation code.</param>
''' <returns>
'''    <c>true</c> if the operation succeeded, <c>false</c> otherwise.
''' </returns>
<DllImport("gdi32.dll")> _
Private Shared Function BitBlt(ByVal hdc As IntPtr, ByVal nXDest As Integer, ByVal nYDest As Integer, ByVal nWidth As Integer, ByVal nHeight As Integer, ByVal hdcSrc As IntPtr, ByVal nXSrc As Integer, ByVal nYSrc As Integer, ByVal dwRop As TernaryRasterOperations) As Boolean
End Function
```

## Tips & Tricks:
```cs
private Bitmap SnapShot(win.Control c)
        {
            Bitmap        bmp;
            IntPtr        dc1;
            IntPtr        dc2;
            Graphics    g;

            bmp=new Bitmap(c.Width, c.Height);
            g=System.Drawing.Graphics.FromImage(bmp);

            dc1=g.GetHdc();
            dc2=GetWindowDC(c.Handle);

            BitBlt(dc1, 0, 0, c.Width, c.Height, dc2, 0, 0, 13369376);

            g.ReleaseHdc(dc1);

            return bmp;
            //bmp.Save(@"c:\snapshot.bmp", System.Drawing.Imaging.ImageFormat.Bmp);
        }
```

## Sample Code:
```cs
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

public enum TernaryRasterOperations : uint {
    SRCCOPY     = 0x00CC0020,
    SRCPAINT    = 0x00EE0086,
    SRCAND      = 0x008800C6,
    SRCINVERT   = 0x00660046,
    SRCERASE    = 0x00440328,
    NOTSRCCOPY  = 0x00330008,
    NOTSRCERASE = 0x001100A6,
    MERGECOPY   = 0x00C000CA,
    MERGEPAINT  = 0x00BB0226,
    PATCOPY     = 0x00F00021,
    PATPAINT    = 0x00FB0A09,
    PATINVERT   = 0x005A0049,
    DSTINVERT   = 0x00550009,
    BLACKNESS   = 0x00000042,
    WHITENESS   = 0x00FF0062,
    CAPTUREBLT  = 0x40000000 //only if WinVer >= 5.0.0 (see wingdi.h)
}

protected override void OnPaint(PaintEventArgs e) {
    IntPtr pTarget = e.Graphics.GetHdc();
    IntPtr pSource = CreateCompatibleDC(pTarget);
    IntPtr pOrig = SelectObject(pSource, bmp.GetHbitmap());
    BitBlt(pTarget, 0,0, bmp.Width, bmp.Height, pSource,0,0,TernaryRasterOperations.SRCCOPY);
    DeleteDC(pSource);
    e.Graphics.ReleaseHdc(pTarget);
}
```
