
## C# Signature:
```cs
[DllImport("uxtheme.dll", EntryPoint = "#120")]
    static extern IntPtr GetUserColorPreference(ref IMMERSIVE_COLOR_PREFERENCE pcpPreference, bool fForceReload);
```

## VB Signature:
```cs
Declare Function GetUserColorPreference Lib "uxtheme.dll" (TODO) As TODO
```

## User-Defined Types:
```cs
private struct IMMERSIVE_COLOR_PREFERENCE
    {
        public uint dwColorSetIndex;
        public uint crStartColor;
        public uint crAccentColor;
    }
```

## Tips & Tricks:
```cs
private static uint ToUint(Color c)
    {
        return (uint)((c.B << 16) | (c.G << 8) | c.R);
    }

    private static Color ToColor(uint c)
    {
        int R = (int)(c & 0xFF) % 256;
        int G = (int)((c >> 8) & 0xFFFF) % 256;
        int B = (int)(c >> 16) % 256;
        return Color.FromArgb(R, G, B);
    }
```

## Sample Code:
```cs
public Color GetAccentColor()
    {
      IMMERSIVE_COLOR_PREFERENCE accent = new();
      GetUserColorPreference(ref accent, false);
      return ToColor(accent.crStartColor);

    }
```
