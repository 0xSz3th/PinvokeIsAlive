
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern IntPtr CreateRoundRectRgn(int x1, int y1, int x2, int y2,
   int cx, int cy);
```

## VBNET Signature :
```cs
<DllImport("Gdi32.dll", EntryPoint:="CreateRoundRectRgn")>
    Private Shared Function CreateRoundRectRgn(ByVal nLeftRect As Integer, ByVal nTopRect As Integer, ByVal nRightRect As Integer, ByVal nBottomRect As Integer, ByVal nWidthEllipse As Integer, ByVal nHeightEllipse As Integer) As IntPtr

    End Function
```

## Sample Code C#:
```cs
private void Form_Paint( object p_SenderObject, System.Windows.Forms.PaintEventArgs p_Arguments )
    {
        IntPtr _RegionHandle = CreateRoundRectRgn( 10, 10, 60, 60, 10, 10 );
        Region _Region = Region.FromHrgn( _RegionHandle );
        p_Arguments.Graphics.FillRegion( new SolidBrush( Color.Black ), _Region );
    }
```

## Sample Code VBNET :
```cs
Protected Overrides Sub OnPaint(ByVal e As PaintEventArgs)

        Region = System.Drawing.Region.FromHrgn(CreateRoundRectRgn(0, 0, Width, Height, Radius_AZ, Radius_AZ))

    MyBase.OnPaint(e)
    End Sub
```
