
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern bool FillRgn(IntPtr hdc, IntPtr hrgn, IntPtr hbr);
```

## Sample Code test:
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

## Sample Code test:
```cs
// This paints the current form black
                IntPtr wDc = GetDC(this.Handle);
                int mx = Screen.PrimaryScreen.WorkingArea.Width;
                int my = Screen.PrimaryScreen.WorkingArea.Height;
                IntPtr brush = CreateSolidBrush(0x0); // black, of format : //0x00bbggrr 
                FillRgn(wDc, CreateRectRgn(0,0,mx,my), brush);
                DeleteObject(brush);
```
