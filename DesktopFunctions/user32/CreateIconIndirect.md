
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern IntPtr CreateIconIndirect([In] ref ICONINFO piconinfo);
```

## Sample Code:
```cs
[StructLayout(LayoutKind.Sequential)]
private struct ICONINFO
{
     public bool IsIcon;
     public int xHotspot;
     public int yHotspot;
     public IntPtr MaskBitmap;
     public IntPtr ColorBitmap;
};

[DllImport("user32.dll")]
private static extern IntPtr CreateIconIndirect([In] ref ICONINFO iconInfo);

[DllImport("gdi32.dll")]
public static extern bool DeleteObject(IntPtr hObject);

private static void CreateIcon()
{
     ICONINFO ii = new ICONINFO();
     ii.IsIcon = true;
     Bitmap img = GetIconBitmap(...);
     IntPtr imgHandle = img.GetHbitmap();
     try
     {
     ii.MaskBitmap = imgHandle;
     ii.ColorBitmap = imgHandle;
     IntPtr handle = CreateIconIndirect(ref ii);
     _formIcon = Icon.FromHandle(handle);
     }
     finally
     {
     DeleteObject(imgHandle);
     }
}
```
