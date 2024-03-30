
## C# Signature:
```cs
[DllImport("uxtheme", EntryPoint = "#122")]
static extern int SetUserColorPreference(ref IMMERSIVE_COLOR_PREFERENCE pcpPreference, bool fForceSetting);
```

## VB Signature:
```cs
Declare Function SetUserColorPreference Lib "uxtheme.dll" (TODO) As TODO
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
[DllImport("uxtheme", EntryPoint = "#122")]
static extern int SetUserColorPreference(ref IMMERSIVE_COLOR_PREFERENCE pcpPreference, bool fForceSetting);

private static uint ToUint(Color c)
{
     return (uint)((c.B << 16) | (c.G << 8) | c.R);
}

[StructLayout(LayoutKind.Sequential)]
  private struct IMMERSIVE_COLOR_PREFERENCE
  {
     public uint dwColorSetIndex;
     public uint crStartColor;
     public uint crAccentColor;
  }

private void SetAccentColor(Color c)
    {
        IMMERSIVE_COLOR_PREFERENCE temp = new IMMERSIVE_COLOR_PREFERENCE
        {
        crAccentColor = ToUint(c),
        dwColorSetIndex = 0,
        crStartColor = ToUint(c)
        };
        SetUserColorPreference(ref temp, true);
    }
```
