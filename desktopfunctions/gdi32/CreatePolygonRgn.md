
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern IntPtr CreatePolygonRgn(POINT [] lppt, int cPoints,
   int fnPolyFillMode);
```

## Tips & Tricks:
```cs
[DllImport("gdi32.dll")]
static extern IntPtr CreatePolygonRgn(Point[] lppt, int cPoints, int fnPolyFillMode);
```

## VBNET Signatute : 
```cs
<DllImport("gdi32.dll")>
    Private Shared Function CreatePolygonRgn(ByVal lppt As Point(), ByVal NumberOfPoints As Integer, ByVal fnPolyFillMode As Integer) As IntPtr

    End Function
```

## Sample Code:
```cs
/// <summary>
/// Create a border for custom label control
/// </summary>
/// <returns>
/// if int is returned. Function was successful.
/// if string is returned. Function was failed.
/// </returns>
/// <remarks>Created by Jim Vazquez Castan. jim.vazquez@gmail.com</remarks>
private string SetBorder()
{
    try
    {
    // First we create polygon
    IntPtr forma = CreatePolygonRgn(edges, edges.Length, 1);
    // then we create area
    int iRes = SetWindowRgn(this.Handle, forma, true);

    return iRes.ToString();
    }
    catch (Exception ex) { return ex.Message; }
}
```
