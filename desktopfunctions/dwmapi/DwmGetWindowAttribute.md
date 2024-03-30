
## C# Signature:
```cs
[DllImport("dwmapi.dll")]
static extern int DwmGetWindowAttribute(IntPtr hwnd, DWMWINDOWATTRIBUTE dwAttribute, out bool pvAttribute, int cbAttribute);

[DllImport("dwmapi.dll")]
static extern int DwmGetWindowAttribute(IntPtr hwnd, DWMWINDOWATTRIBUTE dwAttribute, out RECT pvAttribute, int cbAttribute);
```

## VB Signature:
```cs
Declare Function DwmGetWindowAttribute Lib "dwmapi.dll" (TODO) As TODO
```
