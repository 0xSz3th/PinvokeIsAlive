
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern bool Polygon(IntPtr hdc, POINT [] lpPoints, int nCount);
```

## VB.NET Signature:
```cs
<DllImport("gdi32.dll")> Private Shared Function Polygon( _
    ByVal hdc As Integer, _
    ByRef lpPoint As Object, _
    ByVal nCount As Integer) _
    As Integer

    End Function
```

## Sample Code:
```cs
PostSynchro.Win32.POINTAPI[] TrianglePoints = {new POINT(XStart+5,0),
         new POINT(0, SignalHeight / 2),new POINT(XStart + 5, SignalHeight)};
        PostSynchro.Win32.Polygon(Hdc, TrianglePoints, 3);
```
