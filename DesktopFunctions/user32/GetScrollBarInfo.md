
## C# Signature:
```cs
[DllImport( "user32.dll", SetLastError=true,  EntryPoint="GetScrollBarInfo")]
private static extern int GetScrollBarInfo(IntPtr hWnd, uint idObject, ref SCROLLBARINFO psbi);
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct SCROLLBARINFO
{
    public int cbSize;
    public Rectangle rcScrollBar;
    public int dxyLineButton;
    public int xyThumbTop;
    public int xyThumbBottom;
    public int reserved;
    [MarshalAs(UnmanagedType.ByValArray, SizeConst=6)]
    public int[] rgstate;
}
```

## Notes:
```cs
public struct RECT
{
    public int left;
    public int top;
    public int right;
    public int bottom;
}
```

## Tips & Tricks:
```cs
private const uint OBJID_HSCROLL = 0xFFFFFFFA;
private const uint OBJID_VSCROLL = 0xFFFFFFFB;
private const uint OBJID_CLIENT = 0xFFFFFFFC;
```

## Sample Code:
```cs
SCROLLBARINFO psbi = new SCROLLBARINFO();
psbi.cbSize = Marshal.SizeOf(psbi);

int nResult = GetScrollBarInfo(this.Handle, OBJID_CLIENT, ref psbi); // "this" is a scrollbar

if (nResult == 0)
{
    int nLatError = GetLastError(); // in kernel32.dll
}
```

## Alternative Managed API:
```cs
SystemInformation.HorizontalScrollbar*
```

## Alternative Managed API:
```cs
SystemInformation.VerticalScrollbar*
```
