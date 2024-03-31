
## C# Definition:
```cs
[DllImport("dwmapi.dll")]
    static unsafe extern int DwmGetWindowAttribute(IntPtr hWnd, DwmWindowAttribute dwAttribute, void* pvAttribute, int cbAttribute);
```

## VB Definition:
```cs
Enum DwmGetWindowAttribute
   TODO
End Enum
```

## C# User defined code!!!!
```cs
public enum DwmWindowAttribute {
    DWMWA_NCRENDERING_ENABLED = 1,
    DWMWA_NCRENDERING_POLICY,
    DWMWA_TRANSITIONS_FORCEDISABLED,
    DWMWA_ALLOW_NCPAINT,
    DWMWA_CAPTION_BUTTON_BOUNDS,
    DWMWA_NONCLIENT_RTL_LAYOUT,
    DWMWA_FORCE_ICONIC_REPRESENTATION,
    DWMWA_FLIP3D_POLICY,
    DWMWA_EXTENDED_FRAME_BOUNDS,
    DWMWA_HAS_ICONIC_BITMAP,
    DWMWA_DISALLOW_PEEK,
    DWMWA_EXCLUDED_FROM_PEEK,
    DWMWA_CLOAK,
    DWMWA_CLOAKED,
    DWMWA_FREEZE_REPRESENTATION,
    DWMWA_LAST
    };
```
