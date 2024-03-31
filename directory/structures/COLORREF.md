
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
struct COLORREF {
   public byte R;
   public byte G;
   public byte B;
}

// Alternate
[StructLayout(LayoutKind.Sequential)]
public struct COLORREF
{
   public uint ColorDWORD;

   public COLORREF(System.Drawing.Color color)
   {
      ColorDWORD = (uint) color.R + (((uint) color.G) << 8) + (((uint) color.B) << 16);
   }

   public System.Drawing.Color GetColor()
   {
      return System.Drawing.Color.FromArgb((int) (0x000000FFU & ColorDWORD),
     (int) (0x0000FF00U & ColorDWORD) >> 8, (int) (0x00FF0000U & ColorDWORD) >> 16);
   }

   public void SetColor(System.Drawing.Color color)
   {
      ColorDWORD = (uint) color.R + (((uint) color.G) << 8) + (((uint) color.B) << 16);
   }
}

// Alternate
    [StructLayout(LayoutKind.Explicit, Size = 4)]
    public struct COLORREF {
    public COLORREF(byte r, byte g, byte b) {
        this.Value = 0;
        this.R = r;
        this.G = g;
        this.B = b;
    }

    public COLORREF(uint value) {
        this.R = 0;
        this.G = 0;
        this.B = 0;
        this.Value = value & 0x00FFFFFF;
    }

    [FieldOffset(0)]
    public byte R;
    [FieldOffset(1)]
    public byte G;
    [FieldOffset(2)]
    public byte B;

    [FieldOffset(0)]
    public uint Value;
    }
```

## VB Definition:
```cs
Structure COLORREF 
     Public R As Byte
     Public G As Byte
     Public B As Byte

     Public Overrides Function ToString() As String
     Return String.Format("({0},{1},{2})", R, G, B)
     End Function
End Structure
```

## Notes:
```cs
private static int MakeCOLORREF(byte r, byte g, byte b)
{
    return  (int) (((uint)r) | ( ((uint)g) <<8 ) |  ( ((uint)b) << 16 ));
}
```
