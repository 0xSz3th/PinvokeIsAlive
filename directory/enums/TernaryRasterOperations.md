
## C# Definition:
```cs
/// <summary>
///     Specifies a raster-operation code. These codes define how the color data for the
///     source rectangle is to be combined with the color data for the destination
///     rectangle to achieve the final color.
/// </summary>
enum TernaryRasterOperations : uint {
    /// <summary>dest = source</summary>
    SRCCOPY = 0x00CC0020,
    /// <summary>dest = source OR dest</summary>
    SRCPAINT = 0x00EE0086,
    /// <summary>dest = source AND dest</summary>
    SRCAND = 0x008800C6,
    /// <summary>dest = source XOR dest</summary>
    SRCINVERT = 0x00660046,
    /// <summary>dest = source AND (NOT dest)</summary>
    SRCERASE = 0x00440328,
    /// <summary>dest = (NOT source)</summary>
    NOTSRCCOPY = 0x00330008,
    /// <summary>dest = (NOT src) AND (NOT dest)</summary>
    NOTSRCERASE = 0x001100A6,
    /// <summary>dest = (source AND pattern)</summary>
    MERGECOPY = 0x00C000CA,
    /// <summary>dest = (NOT source) OR dest</summary>
    MERGEPAINT = 0x00BB0226,
    /// <summary>dest = pattern</summary>
    PATCOPY    = 0x00F00021,
    /// <summary>dest = DPSnoo</summary>
    PATPAINT = 0x00FB0A09,
    /// <summary>dest = pattern XOR dest</summary>
    PATINVERT = 0x005A0049,
    /// <summary>dest = (NOT dest)</summary>
    DSTINVERT = 0x00550009,
    /// <summary>dest = BLACK</summary>
    BLACKNESS = 0x00000042,
    /// <summary>dest = WHITE</summary>
    WHITENESS = 0x00FF0062,
    /// <summary>
    /// Capture window as seen on screen.  This includes layered windows 
    /// such as WPF windows with AllowsTransparency="true"
    /// </summary>
    CAPTUREBLT = 0x40000000
}
```

## VB.NET Definition:
```cs
''' <summary>
'''     Specifies a raster-operation code. These codes define how the color data for the
'''     source rectangle is to be combined with the color data for the destination
'''     rectangle to achieve the final color.
''' </summary>
Enum TernaryRasterOperations As UInteger
    ''' <summary>dest = source</summary>
    SRCCOPY = &Hcc0020
    ''' <summary>dest = source OR dest</summary>
    SRCPAINT = &Hee0086
    ''' <summary>dest = source AND dest</summary>
    SRCAND = &H8800c6
    ''' <summary>dest = source XOR dest</summary>
    SRCINVERT = &H660046
    ''' <summary>dest = source AND (NOT dest)</summary>
    SRCERASE = &H440328
    ''' <summary>dest = (NOT source)</summary>
    NOTSRCCOPY = &H330008
    ''' <summary>dest = (NOT src) AND (NOT dest)</summary>
    NOTSRCERASE = &H1100a6
    ''' <summary>dest = (source AND pattern)</summary>
    MERGECOPY = &Hc000ca
    ''' <summary>dest = (NOT source) OR dest</summary>
    MERGEPAINT = &Hbb0226
    ''' <summary>dest = pattern</summary>
    PATCOPY = &Hf00021
    ''' <summary>dest = DPSnoo</summary>
    PATPAINT = &Hfb0a09
    ''' <summary>dest = pattern XOR dest</summary>
    PATINVERT = &H5a0049
    ''' <summary>dest = (NOT dest)</summary>
    DSTINVERT = &H550009
    ''' <summary>dest = BLACK</summary>
    BLACKNESS = &H42
    ''' <summary>dest = WHITE</summary>
    WHITENESS = &Hff0062
    ''' <summary>
    ''' Capture window as seen on screen.  This includes layered windows 
    ''' such as WPF windows with AllowsTransparency="true"
    ''' </summary>
    CAPTUREBLT = &H40000000
End Enum
```
