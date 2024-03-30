
## C# Simple Version:
```cs
// if we specify CharSet.Auto instead of CharSet.Ansi, then the string will be unreadable
        [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto)]
        public class LOGFONT
        {
            public int lfHeight = 0;
            public int lfWidth = 0;
            public int lfEscapement = 0;
            public int lfOrientation = 0;
            public int lfWeight = 0;
            public byte lfItalic = 0;
            public byte lfUnderline = 0;
            public byte lfStrikeOut = 0;
            public byte lfCharSet = 0;
            public byte lfOutPrecision = 0;
            public byte lfClipPrecision = 0;
            public byte lfQuality = 0;
            public byte lfPitchAndFamily = 0;
            [MarshalAs(UnmanagedType.ByValTStr, SizeConst=32)]
            public string lfFaceName = string.Empty;
        }
```

## C# Signature:
```cs
// if we specify CharSet.Auto instead of CharSet.Ansi, then the string will be unreadable
        [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
        public class LOGFONT
        {
            public int lfHeight;
            public int lfWidth;
            public int lfEscapement;
            public int lfOrientation;
            public FontWeight lfWeight;
            [MarshalAs(UnmanagedType.U1)]
            public bool lfItalic;
            [MarshalAs(UnmanagedType.U1)]
            public bool lfUnderline;
            [MarshalAs(UnmanagedType.U1)]
            public bool lfStrikeOut;
            public FontCharSet lfCharSet;
            public FontPrecision lfOutPrecision;
            public FontClipPrecision lfClipPrecision;
            public FontQuality lfQuality;
            public FontPitchAndFamily lfPitchAndFamily;
            [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 32)]
            public string lfFaceName;

            public override string ToString()
            {
                StringBuilder sb = new StringBuilder();
                sb.Append("LOGFONT\n");
                sb.AppendFormat("   lfHeight: {0}\n", lfHeight);
                sb.AppendFormat("   lfWidth: {0}\n", lfWidth);
                sb.AppendFormat("   lfEscapement: {0}\n", lfEscapement);
                sb.AppendFormat("   lfOrientation: {0}\n", lfOrientation);
                sb.AppendFormat("   lfWeight: {0}\n", lfWeight);
                sb.AppendFormat("   lfItalic: {0}\n", lfItalic);
                sb.AppendFormat("   lfUnderline: {0}\n", lfUnderline);
                sb.AppendFormat("   lfStrikeOut: {0}\n", lfStrikeOut);
                sb.AppendFormat("   lfCharSet: {0}\n", lfCharSet);
                sb.AppendFormat("   lfOutPrecision: {0}\n", lfOutPrecision);
                sb.AppendFormat("   lfClipPrecision: {0}\n", lfClipPrecision);
                sb.AppendFormat("   lfQuality: {0}\n", lfQuality);
                sb.AppendFormat("   lfPitchAndFamily: {0}\n", lfPitchAndFamily);
                sb.AppendFormat("   lfFaceName: {0}\n", lfFaceName);

                return sb.ToString();
            }
        }
```

## VB .NET Simple Version:
```cs
<StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Auto)> _
    Public Structure LOGFONT
    Public lfHeight As Int32
    Public lfWidth As Int32
    Public lfEscapement As Int32
    Public lfOrientation As Int32
    Public lfWeight As Int32
    Public lfItalic As Byte
    Public lfUnderline As Byte
    Public lfStrikeOut As Byte
    Public lfCharSet As Byte
    Public lfOutPrecision As Byte
    Public lfClipPrecision As Byte
    Public lfQuality As Byte
    Public lfPitchAndFamily As Byte
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=32)> _
    Public lfFaceName As String
    End Structure
```

## VB .NET Signature:
```cs
<StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Auto)> _
Public Class LOGFONT
     Public lfHeight As Integer
     Public lfWidth As Integer
     Public lfEscapement As Integer
     Public lfOrientation As Integer
     Public lfWeight As FontWeight
     <MarshalAs(UnmanagedType.U1)> _
     Public lfItalic As Boolean
     <MarshalAs(UnmanagedType.U1)> _
     Public lfUnderline As Boolean
     <MarshalAs(UnmanagedType.U1)> _
     Public lfStrikeOut As Boolean
     Public lfCharSet As FontCharSet
     Public lfOutPrecision As FontPrecision
     Public lfClipPrecision As FontClipPrecision
     Public lfQuality As FontQuality
     Public lfPitchAndFamily As FontPitchAndFamily
     <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=32)> _
     Public lfFaceName As String

     Public Overrides Function ToString() As String
     Dim sb As New StringBuilder()
     sb.Append("LOGFONT" & vbLf)
     sb.AppendFormat("   lfHeight: {0}" & vbLf, lfHeight)
     sb.AppendFormat("   lfWidth: {0}" & vbLf, lfWidth)
     sb.AppendFormat("   lfEscapement: {0}" & vbLf, lfEscapement)
     sb.AppendFormat("   lfOrientation: {0}" & vbLf, lfOrientation)
     sb.AppendFormat("   lfWeight: {0}" & vbLf, lfWeight)
     sb.AppendFormat("   lfItalic: {0}" & vbLf, lfItalic)
     sb.AppendFormat("   lfUnderline: {0}" & vbLf, lfUnderline)
     sb.AppendFormat("   lfStrikeOut: {0}" & vbLf, lfStrikeOut)
     sb.AppendFormat("   lfCharSet: {0}" & vbLf, lfCharSet)
     sb.AppendFormat("   lfOutPrecision: {0}" & vbLf, lfOutPrecision)
     sb.AppendFormat("   lfClipPrecision: {0}" & vbLf, lfClipPrecision)
     sb.AppendFormat("   lfQuality: {0}" & vbLf, lfQuality)
     sb.AppendFormat("   lfPitchAndFamily: {0}" & vbLf, lfPitchAndFamily)
     sb.AppendFormat("   lfFaceName: {0}" & vbLf, lfFaceName)

     Return sb.ToString()
     End Function
End Class
```

## C# User-Defined Types:
```cs
public enum FontWeight : int
        {
            FW_DONTCARE = 0,
            FW_THIN = 100,
            FW_EXTRALIGHT = 200,
            FW_LIGHT = 300,
            FW_NORMAL = 400,
            FW_MEDIUM = 500,
            FW_SEMIBOLD = 600,
            FW_BOLD = 700,
            FW_EXTRABOLD = 800,
            FW_HEAVY = 900,
        }
        public enum FontCharSet : byte
        {
            ANSI_CHARSET = 0,
            DEFAULT_CHARSET = 1,
            SYMBOL_CHARSET = 2,
            SHIFTJIS_CHARSET = 128,
            HANGEUL_CHARSET = 129,
            HANGUL_CHARSET = 129,
            GB2312_CHARSET = 134,
            CHINESEBIG5_CHARSET = 136,
            OEM_CHARSET = 255,
            JOHAB_CHARSET = 130,
            HEBREW_CHARSET = 177,
            ARABIC_CHARSET = 178,
            GREEK_CHARSET = 161,
            TURKISH_CHARSET = 162,
            VIETNAMESE_CHARSET = 163,
            THAI_CHARSET = 222,
            EASTEUROPE_CHARSET = 238,
            RUSSIAN_CHARSET = 204,
            MAC_CHARSET = 77,
            BALTIC_CHARSET = 186,
        }
        public enum FontPrecision : byte
        {
            OUT_DEFAULT_PRECIS = 0,
            OUT_STRING_PRECIS = 1,
            OUT_CHARACTER_PRECIS = 2,
            OUT_STROKE_PRECIS = 3,
            OUT_TT_PRECIS = 4,
            OUT_DEVICE_PRECIS = 5,
            OUT_RASTER_PRECIS = 6,
            OUT_TT_ONLY_PRECIS = 7,
            OUT_OUTLINE_PRECIS = 8,
            OUT_SCREEN_OUTLINE_PRECIS = 9,
            OUT_PS_ONLY_PRECIS = 10,
        }
        public enum FontClipPrecision : byte
        {
            CLIP_DEFAULT_PRECIS = 0,
            CLIP_CHARACTER_PRECIS = 1,
            CLIP_STROKE_PRECIS = 2,
            CLIP_MASK = 0xf,
            CLIP_LH_ANGLES = (1 << 4),
            CLIP_TT_ALWAYS = (2 << 4),
            CLIP_DFA_DISABLE = (4 << 4),
            CLIP_EMBEDDED = (8 << 4),
        }
        public enum FontQuality : byte
        {
            DEFAULT_QUALITY = 0,
            DRAFT_QUALITY = 1,
            PROOF_QUALITY = 2,
            NONANTIALIASED_QUALITY = 3,
            ANTIALIASED_QUALITY = 4,
            CLEARTYPE_QUALITY = 5,
            CLEARTYPE_NATURAL_QUALITY = 6,
        }
        [Flags]
        public enum FontPitchAndFamily : byte
        {
            DEFAULT_PITCH = 0,
            FIXED_PITCH = 1,
            VARIABLE_PITCH = 2,
            FF_DONTCARE = (0 << 4),
            FF_ROMAN = (1 << 4),
            FF_SWISS = (2 << 4),
            FF_MODERN = (3 << 4),
            FF_SCRIPT = (4 << 4),
            FF_DECORATIVE = (5 << 4),
        }
```

## VB .NET User-Defined Types:
```cs
Public Enum FontWeight As Integer
        FW_DONTCARE = 0
        FW_THIN = 100
        FW_EXTRALIGHT = 200
        FW_LIGHT = 300
        FW_NORMAL = 400
        FW_MEDIUM = 500
        FW_SEMIBOLD = 600
        FW_BOLD = 700
        FW_EXTRABOLD = 800
        FW_HEAVY = 900
    End Enum

    Public Enum FontCharSet As Byte
        ANSI_CHARSET = 0
        DEFAULT_CHARSET = 1
        SYMBOL_CHARSET = 2
        SHIFTJIS_CHARSET = 128
        HANGEUL_CHARSET = 129
        HANGUL_CHARSET = 129
        GB2312_CHARSET = 134
        CHINESEBIG5_CHARSET = 136
        OEM_CHARSET = 255
        JOHAB_CHARSET = 130
        HEBREW_CHARSET = 177
        ARABIC_CHARSET = 178
        GREEK_CHARSET = 161
        TURKISH_CHARSET = 162
        VIETNAMESE_CHARSET = 163
        THAI_CHARSET = 222
        EASTEUROPE_CHARSET = 238
        RUSSIAN_CHARSET = 204
          MAC_CHARSET = 77
        BALTIC_CHARSET = 186
    End Enum

    Public Enum FontPrecision As Byte
        OUT_DEFAULT_PRECIS = 0
        OUT_STRING_PRECIS = 1
        OUT_CHARACTER_PRECIS = 2
        OUT_STROKE_PRECIS = 3
        OUT_TT_PRECIS = 4
        OUT_DEVICE_PRECIS = 5
        OUT_RASTER_PRECIS = 6
        OUT_TT_ONLY_PRECIS = 7
        OUT_OUTLINE_PRECIS = 8
        OUT_SCREEN_OUTLINE_PRECIS = 9
        OUT_PS_ONLY_PRECIS = 10
    End Enum

    Public Enum FontClipPrecision As Byte
        CLIP_DEFAULT_PRECIS = 0
        CLIP_CHARACTER_PRECIS = 1
        CLIP_STROKE_PRECIS = 2
        CLIP_MASK = &HF
        CLIP_LH_ANGLES = (1 << 4)
        CLIP_TT_ALWAYS = (2 << 4)
        CLIP_DFA_DISABLE = (4 << 4)
        CLIP_EMBEDDED = (8 << 4)
    End Enum

    Public Enum FontQuality As Byte
        DEFAULT_QUALITY = 0
        DRAFT_QUALITY = 1
        PROOF_QUALITY = 2
        NONANTIALIASED_QUALITY = 3
        ANTIALIASED_QUALITY = 4
        CLEARTYPE_QUALITY = 5
        CLEARTYPE_NATURAL_QUALITY = 6
    End Enum

    Public Enum FontPitchAndFamily As Byte
        DEFAULT_PITCH = 0
        FIXED_PITCH = 1
        VARIABLE_PITCH = 2
        FF_DONTCARE = (0 << 4)
        FF_ROMAN = (1 << 4)
        FF_SWISS = (2 << 4)
        FF_MODERN = (3 << 4)
        FF_SCRIPT = (4 << 4)
        FF_DECORATIVE = (5 << 4)
    End Enum
```

## Sample Code:
```cs
// =========================================================================
        // EXAMPLE 1 - Filling a Font object with a LOGFONT.
        //        [in]    LayoutDesign.CtlLayout (ActiveX control)
        //        [out]    fontReceived (System.Drawing.Font)

        // An ActiveX control returns a handle to a LOGFONT in unmanaged global mem.
          IntPtr hHGlobalLOGFONT = (IntPtr)LayoutDesign.CtlLayout.BorderTextLogfont;

        // Stake a claim to the memory and get a pointer to it.
          IntPtr pLOGFONT = DLLKernel32.GlobalLock(hHGlobalLOGFONT);

        // Instantiate a managed logical font struct (as defined above!)
          LOGFONT lf = new LOGFONT();

        // Copy the LOGFONT data into managed mem.
        Marshal.PtrToStructure(pLOGFONT, lf);

        // Create the Font object.
        Font fontReceived = Font.FromLogFont(lf);

        // Release the claim to the global mem.
          DLLKernel32.GlobalUnlock(hHGlobalLOGFONT);

        // ... Do whatever with the Font object "fontReceived" ...

        // =========================================================================
        // EXAMPLE 2 - Reversing the process.
        //        [in]    fontReceived (System.Drawing.Font)
        //        [out]    LayoutDesign.CtlLayout (ActiveX control)

        // Use the ActiveX's global memory.
          IntPtr hHGlobalLOGFONT = (IntPtr)LayoutDesign.CtlLayout.BorderTextLogfont;

        // Stake a claim to the memory and get a pointer to it.
          IntPtr pLOGFONT = DLLKernel32.GlobalLock(hHGlobalLOGFONT);

        // Instantiate a managed logical font struct (as defined above!)
          LOGFONT lf = new LOGFONT();

        // Load the LOGFONT struct from the managed Font object.
        fontReceived.ToLogFont(lf);

        // Copy the LOGFONT data into managed mem.
        Marshal.StructureToPtr(pLOGFONT, lf, false);

        // Release the claim to the global mem.
          DLLKernel32.GlobalUnlock(hHGlobalLOGFONT);

        // Update the ActiveX control.
        (IntPtr)LayoutDesign.CtlLayout.BorderTextLogfont = hHGlobalLOGFONT;
```
