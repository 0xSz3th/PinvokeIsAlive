
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern bool GetTextExtentPoint32(IntPtr hdc, string lpString,
   int cbString, out SIZE lpSize);
```

## Tips & Tricks:
```cs
int cbString, out SIZE lpSize);
```

## Sample Code:
```cs
Size sz = Size.Empty;
    IntPtr hdc = graphics.GetHdc();
    IntPtr oldfnt = GDI.SelectObject(hdc, font.ToHfont());

    GDI.GetTextExtentPoint32(hdc, text, text.Length,out sz);

    // reset old font
    GDI.DeleteObject(GDI.SelectObject(hdc, oldfnt));
    graphics.ReleaseHdc(hdc);
    return sz;
```

## Alternative Managed API:
```cs
using System.Windows.Forms; // for TextRenderer

    Size size=TextRenderer.MeasureText(g, str, f, new Size(), TextFormatFlags.NoPadding);
```

## Alternative Managed API:
```cs
g - is the Graphics object you want to draw on
    str - the string that should be measured
    f - the font you want to use
    new Size() - just a dummy parameter
```
