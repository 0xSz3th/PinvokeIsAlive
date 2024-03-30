
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern IntPtr CreateFont(int nHeight, int nWidth, int nEscapement,
   int nOrientation, int fnWeight, uint fdwItalic, uint fdwUnderline, uint
   fdwStrikeOut, uint fdwCharSet, uint fdwOutputPrecision, uint
   fdwClipPrecision, uint fdwQuality, uint fdwPitchAndFamily, string lpszFace);
```

## C# Signature:
```cs
[DllImport("gdi32", EntryPoint="CreateFontW")]
static extern IntPtr CreateFontW(
            [In] Int32 nHeight,
            [In] Int32 nWidth,
            [In] Int32 nEscapement,
            [In] Int32 nOrientation,
            [In] Int32 fnWeight,
            [In] UInt32 fdwItalic,
            [In] UInt32 fdwUnderline,
            [In] UInt32 fdwStrikeOut,
            [In] UInt32 fdwCharSet,
            [In] UInt32 fdwOutputPrecision,
            [In] UInt32 fdwClipPrecision,
            [In] UInt32 fdwQuality,
            [In] UInt32 fdwPitchAndFamily,
            [In] IntPtr lpszFace);
```

## vb.net Signature:
```cs
Private Declare Function CreateFont Lib "gdi32" Alias "CreateFontA" (_
    ByVal nHeight As Int32, ByVal nWidth As Int32, _
    ByVal nEscapement As Int32, ByVal nOrientation As Int32, _
    ByVal fnWeight As Int32, ByVal fdwItalic As UInt32, _
    ByVal fdwUnderline As UInt32, ByVal fdwStrikeOut As UInt32, _
    ByVal fdwCharSet As Int32, ByVal fdwOutputPrecision As UInt32, _
    ByVal fdwClipPrecision As UInt32, ByVal fdwQuality As UInt32, _
    ByVal fdwPitchAndFamily As UInt32, ByVal lpszFace As String _
    ) As IntPtr
```
