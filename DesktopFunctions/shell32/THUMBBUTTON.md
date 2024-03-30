
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, Pack = 8, CharSet = CharSet.Unicode)]
public struct THUMBBUTTON
{
    public THUMBBUTTONMASK dwMask;
    public uint iId;
    public uint iBitmap;
    public IntPtr hIcon;

    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 259)]
    public string szTip;

    public THUMBBUTTONFLAGS dwFlags;
}
```

## VB Definition:
```cs
Structure THUMBBUTTON
   Public TODO
End Structure
```
