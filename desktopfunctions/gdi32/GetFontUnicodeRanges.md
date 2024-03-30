
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern uint GetFontUnicodeRanges(IntPtr hdc, IntPtr lpgs);
```

## Sample Code:
```cs
[DllImport("gdi32.dll")]
    public static extern uint GetFontUnicodeRanges(IntPtr hdc, IntPtr lpgs);

    [DllImport("gdi32.dll")]
    public extern static IntPtr SelectObject(IntPtr hDC, IntPtr hObject);

    public struct FontRange
    {
        public UInt16 Low;
        public UInt16 High;
    }

    public List<FontRange> GetFontUnicodeRanges(Font font)
    {
        Graphics g = Graphics.FromHwnd(IntPtr.Zero);
        IntPtr hdc = g.GetHdc();
        IntPtr hFont = font.ToHfont();
        IntPtr old = SelectObject(hdc, hFont);
        uint size = GetFontUnicodeRanges(hdc, IntPtr.Zero);
        IntPtr glyphSet = Marshal.AllocHGlobal((int)size);
        GetFontUnicodeRanges(hdc, glyphSet);
        List<FontRange> fontRanges = new List<FontRange>();
        int count = Marshal.ReadInt32(glyphSet, 12);
        for (int i = 0; i < count; i++)
        {
        FontRange range = new FontRange();
        range.Low = (UInt16)Marshal.ReadInt16(glyphSet, 16 + i * 4);
        range.High = (UInt16)(range.Low + Marshal.ReadInt16(glyphSet, 18 + i * 4) - 1);
        fontRanges.Add(range);
        }
        SelectObject(hdc, old);
        Marshal.FreeHGlobal(glyphSet);
        g.ReleaseHdc(hdc);
        g.Dispose();
        return fontRanges;
    }
```
