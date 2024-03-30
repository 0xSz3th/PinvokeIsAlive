
## C# Definition:
```cs
public const int MAX_PATH = 260;

[StructLayoutAttribute(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
public struct SHSTOCKICONINFO
{
    public UInt32 cbSize;
    public IntPtr hIcon;
    public Int32 iSysIconIndex;
    public Int32 iIcon;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = MAX_PATH)]
    public string szPath;
}
```

## VB Definition:
```cs
<StructLayoutAttribute(LayoutKind.Sequential, CharSet:=CharSet.Unicode)> _
    Public Structure SHSTOCKICONINFO
    Public cbSize As UInt32
    Public hIcon As IntPtr
    Public iSysIconIndex As Int32
    Public iIcon As Int32
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=MAX_PATH)> _
    Public szPath As String
    End Structure
```
