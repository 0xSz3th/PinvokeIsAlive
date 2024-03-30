
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern uint SetPixel(IntPtr hdc, int X, int Y, uint crColor);
```

## Sample Code:
```cs
return crColor.B << 16 | crColor.G << 8 | crColor.R;
```

## Sample Code:
```cs
Graphics vGraphics = Graphics.FromHwnd(Handle);
    SetPixel(vGraphics.GetHdc(), 10, 10, ColorToRGB(Color.Red));
```
