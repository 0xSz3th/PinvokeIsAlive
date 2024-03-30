
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern bool RoundRect(IntPtr hdc, int nLeftRect, int nTopRect,
   int nRightRect, int nBottomRect, int nWidth, int nHeight);
```

## Sample Code:
```cs
public class GDI32
{
    #region GDI32 Functions
    [DllImport("gdi32.dll")]
    public static extern bool RoundRect(RECT lpRect, Point point); 

    [DllImport("gdi32.dll")]
    public static extern bool RoundRect(IntPtr hdc, int nLeftRect, int nTopRect,
    int nRightRect, int nBottomRect, int nWidth, int nHeight);

    [DllImport("gdi32.dll")]
    public static extern IntPtr CreateSolidBrush(uint crColor);

    [DllImport("gdi32.dll")]
    public static extern IntPtr CreatePen(int fnPenStyle, int nWidth, uint crColor);

    [DllImport("gdi32.dll")]
    public static extern IntPtr SelectObject(IntPtr hdc, IntPtr hgdiobj);

    [DllImport("gdi32.dll")]
    public static extern bool DeleteObject(IntPtr hObject);

    public static int RGB(Color color)
    {
        return color.ToArgb() & 0xffffff;
    }

    #endregion
}

public class RoundControl : System.Windows.Forms.Control
{
    protected override void OnPaint(PaintEventArgs e)
    {
        DrawRoundRect(e.Graphics);
    }

    public void DrawRoundRect(Graphics gr)
    {            
        RECT rect = new RECT(0, 0, this.Width, this.Height);
        IntPtr hDC = gr.GetHdc();
        IntPtr thePen = GDI32.CreatePen(0, 1, (uint)GDI32.RGB(Color.White));
        IntPtr theBrush = GDI32.CreateSolidBrush((uint)GDI32.RGB(Color.White));
        IntPtr oldPen = GDI32.SelectObject(hDC, thePen);
        IntPtr oldBrush = GDI32.SelectObject(hDC, theBrush);        

        GDI32.RoundRect(hDC, 0, 0, this.Width, this.Height, 20, 20);

        GDI32.SelectObject(hDC, oldPen);
        GDI32.DeleteObject(thePen);
        GDI32.SelectObject(hDC, oldBrush);            
        GDI32.DeleteObject(theBrush);

        gr.ReleaseHdc(hDC);            
    }
}
```
