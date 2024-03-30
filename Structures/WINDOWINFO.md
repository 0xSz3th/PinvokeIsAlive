
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
struct WINDOWINFO
{
    public uint cbSize;
    public RECT rcWindow;
    public RECT rcClient;
    public uint dwStyle;
    public uint dwExStyle;
    public uint dwWindowStatus;
    public uint cxWindowBorders;
    public uint cyWindowBorders;
    public ushort atomWindowType;
    public ushort wCreatorVersion;

    public WINDOWINFO(Boolean ?   filler)   :   this()   // Allows automatic initialization of "cbSize" with "new WINDOWINFO(null/true/false)".
    {
        cbSize = (UInt32)(Marshal.SizeOf(typeof( WINDOWINFO )));
    }

}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)> Structure WINDOWINFO
    Dim cbSize As Integer
    Dim rcWindow As RECT
    Dim rcClient As RECT
    Dim dwStyle As Integer
    Dim dwExStyle As Integer
    Dim dwWindowStatus As UInt32
    Dim cxWindowBorders As UInt32
    Dim cyWindowBorders As UInt32
    Dim atomWindowType As UInt16
    Dim wCreatorVersion As Short
End Structure
```
