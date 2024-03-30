
## C# Definition:
```cs
public int cbSize;
    public int dwMask;
    public int dwEffects;
    public int yHeight;
    public int yOffset;
    public int crTextColor;
    public byte bCharSet;
    public byte bPitchAndFamily;
    [MarshalAs( UnmanagedType.ByValTStr, SizeConst=32 )]
    public string szFaceName;
    public short wWeight;
    public short sSpacing;
    public int crBackColor;
    public int lcid;
    public int dwReserved;
    public short sStyle;
    public short wKerning;
    public byte bUnderlineType;
    public byte bAnimation;
    public byte bRevAuthor;
    public byte bReserved1;
```

## VB Definition:
```cs
Public cbSize As Integer
    Public dwMask As Integer
    Public dwEffects As Integer
    Public yHeight As Integer
    Public yOffset As Integer
    Public crTextColor As Integer
    Public bCharSet As Byte
    Public bPitchAndFamily As Byte
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst := 32)> _
    Public szFaceName As String
    Public wWeight As Short
    Public sSpacing As Short
    Public crBackColor As Integer
    Public lcid As Integer
    Public dwReserved As Integer
    Public sStyle As Short
    Public wKerning As Short
    Public bUnderlineType As Byte
    Public bAnimation As Byte
    Public bRevAuthor As Byte
    Public bReserved1 As Byte
```
