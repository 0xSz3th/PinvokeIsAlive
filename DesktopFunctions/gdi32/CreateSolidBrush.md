
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern IntPtr CreateSolidBrush(uint crColor);
```

## VB.NET Signature:
```cs
<DllImport("gdi32.dll")> _
Private Shared Function CreateSolidBrush(crColor As UInteger) As IntPtr
End Function
```

## Sample Code:
```cs
[DllImport("user32.dll",EntryPoint="GetDC")]
        static extern IntPtr GetDC(IntPtr hWnd);

        [DllImport("gdi32.dll")]
        static extern bool FillRgn(IntPtr hdc, IntPtr hrgn, IntPtr hbr);

        [DllImport("gdi32.dll")]
        static extern IntPtr CreateRectRgn(int nLeftRect, int nTopRect, int nRightRect,
            int nBottomRect);

        [DllImport("gdi32.dll")]
        static extern IntPtr CreateSolidBrush(uint crColor);

        [DllImport("gdi32.dll")]
        static extern bool DeleteObject(IntPtr hObject);
```

## Sample Code:
```cs
// This paints the current form black
                IntPtr wDc = GetDC(this.Handle);
                int mx = Screen.PrimaryScreen.WorkingArea.Width;
                int my = Screen.PrimaryScreen.WorkingArea.Height;
                IntPtr brush = CreateSolidBrush((uint)ColorTranslator.ToWin32(Color.Black)); 
                FillRgn(wDc, CreateRectRgn(0,0,mx,my), brush);
                DeleteObject(brush);
```
