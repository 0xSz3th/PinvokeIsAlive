
## C# Definition:
```cs
[Serializable, StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
public struct TEXTMETRIC
{
    public int tmHeight;
    public int tmAscent;
    public int tmDescent;
    public int tmInternalLeading;
    public int tmExternalLeading;
    public int tmAveCharWidth;
    public int tmMaxCharWidth;
    public int tmWeight;
    public int tmOverhang;
    public int tmDigitizedAspectX;
    public int tmDigitizedAspectY;
    public byte tmFirstChar;    // this assumes the ANSI charset; for the UNICODE charset the type is char (or short)
    public byte tmLastChar;     // this assumes the ANSI charset; for the UNICODE charset the type is char (or short)
    public byte tmDefaultChar;  // this assumes the ANSI charset; for the UNICODE charset the type is char (or short)
    public byte tmBreakChar;    // this assumes the ANSI charset; for the UNICODE charset the type is char (or short)
    public byte tmItalic;
    public byte tmUnderlined;
    public byte tmStruckOut;
    public byte tmPitchAndFamily;
    public byte tmCharSet;
}

[Serializable, StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
public struct TEXTMETRICW
{
    public int tmHeight;
    public int tmAscent;
    public int tmDescent;
    public int tmInternalLeading;
    public int tmExternalLeading;
    public int tmAveCharWidth;
    public int tmMaxCharWidth;
    public int tmWeight;
    public int tmOverhang;
    public int tmDigitizedAspectX;
    public int tmDigitizedAspectY;
    public ushort tmFirstChar;
    public ushort tmLastChar;
    public ushort tmDefaultChar;
    public ushort tmBreakChar;
    public byte tmItalic;
    public byte tmUnderlined;
    public byte tmStruckOut;
    public byte tmPitchAndFamily;
    public byte tmCharSet;
}

[Serializable, StructLayout(LayoutKind.Sequential, CharSet=CharSet.Ansi)]
public struct TEXTMETRICA
{
    public int tmHeight;
    public int tmAscent;
    public int tmDescent;
    public int tmInternalLeading;
    public int tmExternalLeading;
    public int tmAveCharWidth;
    public int tmMaxCharWidth;
    public int tmWeight;
    public int tmOverhang;
    public int tmDigitizedAspectX;
    public int tmDigitizedAspectY;
    public byte tmFirstChar;
    public byte tmLastChar;
    public byte tmDefaultChar;
    public byte tmBreakChar;
    public byte tmItalic;
    public byte tmUnderlined;
    public byte tmStruckOut;
    public byte tmPitchAndFamily;
    public byte tmCharSet;
}
```

## VB Definition
```cs
<Serializable(), StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Auto)> _
Public Structure TEXTMETRIC
    Public tmHeight As Int32
    Public tmAscent As Int32
    Public tmDescent As Int32
    Public tmInternalLeading As Int32
    Public tmExternalLeading As Int32
    Public tmAveCharWidth As Int32
    Public tmMaxCharWidth As Int32
    Public tmWeight As Int32
    Public tmOverhang As Int32
    Public tmDigitizedAspectX As Int32
    Public tmDigitizedAspectY As Int32
    Public tmFirstChar As Char
    Public tmLastChar As Char
    Public tmDefaultChar As Char
    Public tmBreakChar As Char
    Public tmItalic As Byte
    Public tmUnderlined As Byte
    Public tmStruckOut As Byte
    Public tmPitchAndFamily As Byte
    Public tmCharSet As Byte
End Structure

<Serializable(), StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Unicode)> _
Public Structure TEXTMETRICW
    Public tmHeight As Int32
    Public tmAscent As Int32
    Public tmDescent As Int32
    Public tmInternalLeading As Int32
    Public tmExternalLeading As Int32
    Public tmAveCharWidth As Int32
    Public tmMaxCharWidth As Int32
    Public tmWeight As Int32
    Public tmOverhang As Int32
    Public tmDigitizedAspectX As Int32
    Public tmDigitizedAspectY As Int32
    Public tmFirstChar As UShort
    Public tmLastChar As UShort
    Public tmDefaultChar As UShort
    Public tmBreakChar As UShort
    Public tmItalic As Byte
    Public tmUnderlined As Byte
    Public tmStruckOut As Byte
    Public tmPitchAndFamily As Byte
    Public tmCharSet As Byte
End Structure

<Serializable(), StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Ansi)> _
Public Structure TEXTMETRICA
    Public tmHeight As Int32
    Public tmAscent As Int32
    Public tmDescent As Int32
    Public tmInternalLeading As Int32
    Public tmExternalLeading As Int32
    Public tmAveCharWidth As Int32
    Public tmMaxCharWidth As Int32
    Public tmWeight As Int32
    Public tmOverhang As Int32
    Public tmDigitizedAspectX As Int32
    Public tmDigitizedAspectY As Int32
    Public tmFirstChar As Char
    Public tmLastChar As Char
    Public tmDefaultChar As Char
    Public tmBreakChar As Char
    Public tmItalic As Byte
    Public tmUnderlined As Byte
    Public tmStruckOut As Byte
    Public tmPitchAndFamily As Byte
    Public tmCharSet As Byte
End Structure
```
