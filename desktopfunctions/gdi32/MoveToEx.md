
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern bool MoveToEx(IntPtr hdc, int X, int Y, IntPtr lpPoint);
```

## Sample Code:
```cs
IntPtr pTarget = maskg.GetHdc();
    IntPtr pDC = CreateCompatibleDC(pTarget);
    IntPtr pOrig = SelectObject(pDC, hbitmap);

    Color penColor = Color.Blue;
    int penWidth = 20;

    IntPtr pen = CreatePen(PenStyle.PS_SOLID | PenStyle.PS_GEOMETRIC | PenStyle.PS_ENDCAP_ROUND, penWidth, (uint)ColorTranslator.ToWin32(penColor));

    // select the pen into the device context
    IntPtr oldpen = SelectObject(pDC, pen);

    MoveToEx(pDC, start.X, start.Y, IntPtr.Zero);
    LineTo(pDC, end.X, end.Y);

    // select the old pen back
    DeleteObject(SelectObject(pDC, oldpen));
    SelectObject(pDC, pOrig);
    maskg.ReleaseHdc();
```
