
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern int EnumFontFamiliesEx(IntPtr hdc, [In] ref LOGFONT lpLogfont,
   EnumFontExDelegate lpEnumFontFamExProc, IntPtr lParam, uint dwFlags);
```

## Sample Code:
```cs
private const byte DEFAULT_CHARSET = 1;
    private const byte SHIFTJIS_CHARSET = 128;
    private const byte JOHAB_CHARSET = 130;
    private const byte EASTEUROPE_CHARSET = 238;
    private const byte DEFAULT_PITCH = 0;
    private const byte FIXED_PITCH = 1;
    private const byte VARIABLE_PITCH = 2;
    private const byte FF_DONTCARE = (0 << 4);
    private const byte FF_ROMAN = (1 << 4);
    private const byte FF_SWISS = (2 << 4);
    private const byte FF_MODERN = (3 << 4);
    private const byte FF_SCRIPT = (4 << 4);
    private const byte FF_DECORATIVE = (5 << 4);

    private List<FontFamily> _fonts = new List<FontFamily>();

    public List<FontFamily> FontFamilies
    {
    get { return _fonts; }
    set { _fonts = value; }
    }

    public void GetFonts()
    {
    LOGFONT lf = CreateLogFont("");

    IntPtr plogFont = Marshal.AllocHGlobal(Marshal.SizeOf(lf));
    Marshal.StructureToPtr(lf, plogFont, true);

    int ret = 0;
    try
    {
        //If anyone knows of a better way to get the pointer please let me know
        var pictureBox = new PictureBox();
        var graphic = pictureBox.CreateGraphics();
        var ptr = graphic.GetHdc();

        del1 = new EnumFontExDelegate(callback1);
        ret = EnumFontFamiliesEx(ptr, plogFont, del1, IntPtr.Zero, 0);

        System.Diagnostics.Trace.WriteLine("EnumFontFamiliesEx = " + ret.ToString());

        graphic.ReleaseHdc(ptr);
    }
    catch
    {
        System.Diagnostics.Trace.WriteLine("Error!");
    }
    finally
    {
        Marshal.DestroyStructure(plogFont, typeof(LOGFONT));

    }
    }

    [DllImport("gdi32.dll", CharSet = CharSet.Auto)]
    static extern int EnumFontFamiliesEx(IntPtr hdc,
                [In] IntPtr pLogfont,
                EnumFontExDelegate lpEnumFontFamExProc,
                IntPtr lParam,
                uint dwFlags);

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
    }

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

    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
    public struct NEWTEXTMETRIC
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
    public char tmFirstChar;
    public char tmLastChar;
    public char tmDefaultChar;
    public char tmBreakChar;
    public byte tmItalic;
    public byte tmUnderlined;
    public byte tmStruckOut;
    public byte tmPitchAndFamily;
    public byte tmCharSet;
    int ntmFlags;
    int ntmSizeEM;
    int ntmCellHeight;
    int ntmAvgWidth;
    }
    public struct FONTSIGNATURE
    {
    [MarshalAs(UnmanagedType.ByValArray)]
    int[] fsUsb;
    [MarshalAs(UnmanagedType.ByValArray)]
    int[] fsCsb;
    }
    public struct NEWTEXTMETRICEX
    {
    NEWTEXTMETRIC ntmTm;
    FONTSIGNATURE ntmFontSig;
    }

    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
    public struct ENUMLOGFONTEX
    {
    public LOGFONT elfLogFont;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 64)]
    public string elfFullName;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 32)]
    public string elfStyle;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 32)]
    public string elfScript;
    }

    public delegate int EnumFontExDelegate(ref ENUMLOGFONTEX lpelfe, ref NEWTEXTMETRICEX lpntme, int FontType, int lParam);
    public EnumFontExDelegate del1;

    public int callback1(ref ENUMLOGFONTEX lpelfe, ref NEWTEXTMETRICEX lpntme, int FontType, int lParam)
    {
    try
    {
        FontType fontType;
        if (FontType == 2 || FontType == 4)
        {
        fontType = (ClientTools.Fonts.FontType)FontType;
        }
        else
        {
        fontType = ClientTools.Fonts.FontType.Unknown;
        }

        FontFamilies.Add(new FontFamily(lpelfe.elfFullName, fontType));
    }
    catch (Exception e)
    {
        System.Diagnostics.Trace.WriteLine(e.ToString());
    }
    return 1;
    }

    public static LOGFONT CreateLogFont(string fontname)
    {
    LOGFONT lf = new LOGFONT();
    lf.lfHeight = 0;
    lf.lfWidth = 0;
    lf.lfEscapement = 0;
    lf.lfOrientation = 0;
    lf.lfWeight = 0;
    lf.lfItalic = false;
    lf.lfUnderline = false;
    lf.lfStrikeOut = false;
    lf.lfCharSet = FontCharSet.DEFAULT_CHARSET;
    lf.lfOutPrecision = 0;
    lf.lfClipPrecision = 0;
    lf.lfQuality = 0;
    lf.lfPitchAndFamily = FontPitchAndFamily.FF_DONTCARE;
    lf.lfFaceName = "";
```

## Sample Code:
```cs
return lf;
    }
```

## Sample Code:
```cs
public string FontName { get; set; }

    public FontType FontType { get; set; }

    public FontFamily(string fontName, FontType fontType)
    {
    FontName = fontName;
    FontType = fontType;
    }
```

## Sample Code:
```cs
Unknown = 1,
    TrueType = 4,
    PostScript = 2
```

## Sample Code: (Tested on Windows 8.1 Professional 64 Bit)
```cs
internal static class GdiFonts
    {

        #region gdi32

        /// <summary>
        /// From WinGDI.h
        /// #define RASTER_FONTTYPE     0x0001
        /// #define DEVICE_FONTTYPE     0x0002
        /// #define TRUETYPE_FONTTYPE   0x0004
        /// </summary>
        public enum FontMask
        {
            RASTER_FONTTYPE = 0x0001,
            DEVICE_FONTTYPE = 0x0002,
            TRUETYPE_FONTTYPE = 0x0004
        }

        /// <summary>
        /// From WinGDI.h
        /// #define FW_DONTCARE     0
        /// #define FW_THIN         100
        /// #define FW_EXTRALIGHT       200
        /// #define FW_LIGHT        300
        /// #define FW_NORMAL       400
        /// #define FW_MEDIUM       500
        /// #define FW_SEMIBOLD     600
        /// #define FW_BOLD         700
        /// #define FW_EXTRABOLD    800
        /// #define FW_HEAVY        900
        /// #define FW_ULTRALIGHT       FW_EXTRALIGHT
        /// #define FW_REGULAR      FW_NORMAL
        /// #define FW_DEMIBOLD     FW_SEMIBOLD
        /// #define FW_ULTRABOLD    FW_EXTRABOLD
        /// #define FW_BLACK        FW_HEAVY
        /// </summary>
        public enum FontWeight
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
            FW_HEAVY = 900
        }

        /// <summary>
        /// From WinGDI.h
        ///    #define DEFAULT_PITCH       0
        /// #define FIXED_PITCH         1
        /// #define VARIABLE_PITCH      2
        /// #if(WINVER >= 0x0400)
        /// #define MONO_FONT           8
        /// #endif /* WINVER >= 0x0400 */
        /// </summary>
        public enum FontPitch : int
        {
            DEFAULT_PITCH = 0,
            FIXED_PITCH = 1,
            VARIABLE_PITCH = 2,
            MONO_FONT = 8
        }

        /// <summary>
        /// From WinGDI.h
        /// #define FF_DONTCARE     (0<<4)  Don't care or don't know.
        /// #define FF_ROMAN        (1<<4)  Variable stroke width, serifed.
        ///                                        Times Roman, Century Schoolbook, etc.
        /// #define FF_SWISS        (2<<4)  Variable stroke width, sans-serifed.
        ///                                        Helvetica, Swiss, etc.
        /// #define FF_MODERN       (3<<4)  Constant stroke width, serifed or sans-serifed.
        ///                                        Pica, Elite, Courier, etc.
        /// #define FF_SCRIPT       (4<<4)  Cursive, etc.
        /// #define FF_DECORATIVE       (5<<4)  Old English, etc.
        /// </summary>
        public enum FontFamily
        {
            FF_DONTCARE = 0 << 4,
            FF_ROMAN = 1 << 4,
            FF_SWISS = 2 << 4,
            FF_MODERN = 3 << 4,
            FF_SCRIPT = 4 << 4,
            FF_DECORATIVE = 5 << 4
        }

        /// <summary>
        /// From WinGDI.h
        /// #define MM_TEXT         1
        /// #define MM_LOMETRIC     2
        /// #define MM_HIMETRIC     3
        /// #define MM_LOENGLISH    4
        /// #define MM_HIENGLISH    5
        /// #define MM_TWIPS        6
        /// #define MM_ISOTROPIC    7
        /// #define MM_ANISOTROPIC      8
        /// </summary>
        public enum FontMappingMode
        {
            MM_TEXT = 1,
            MM_LOMETRIC = 2,
            MM_HIMETRIC = 3,
            MM_LOENGLISH = 4,
            MM_HIENGLISH = 5,
            MM_TWIPS = 6,
            MM_ISOTROPIC = 7,
            MM_ANISOTROPIC = 8
        }

        public enum FontLanguageCharSet
        {
            ANSI_CHARSET = 0x00000000,
            DEFAULT_CHARSET = 0x00000001,
            SYMBOL_CHARSET = 0x00000002,
            MAC_CHARSET = 0x0000004D,
            SHIFTJIS_CHARSET = 0x00000080,
            HANGUL_CHARSET = 0x00000081,
            JOHAB_CHARSET = 0x00000082,
            GB2312_CHARSET = 0x00000086,
            CHINESEBIG5_CHARSET = 0x00000088,
            GREEK_CHARSET = 0x000000A1,
            TURKISH_CHARSET = 0x000000A2,
            VIETNAMESE_CHARSET = 0x000000A3,
            HEBREW_CHARSET = 0x000000B1,
            ARABIC_CHARSET = 0x000000B2,
            BALTIC_CHARSET = 0x000000BA,
            RUSSIAN_CHARSET = 0x000000CC,
            THAI_CHARSET = 0x000000DE,
            EASTEUROPE_CHARSET = 0x000000EE,
            OEM_CHARSET = 0x000000FF
        }

        public const Int32 LF_FACESIZE = 32; // ref WinGDI.h
        public const Int32 LF_FULLFACESIZE = 64; // ref WinGDI.h

        [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
        public struct LOGFONT
        {
            public Int32 lfHeight;
            public Int32 lfWidth;
            public Int32 lfEscapement;
            public Int32 lfOrientation;
            public Int32 lfWeight;
            public Byte lfItalic;
            public Byte lfUnderline;
            public Byte lfStrikeOut;
            public Byte lfCharSet;
            public Byte lfOutPrecision;
            public Byte lfClipPrecision;
            public Byte lfQuality;
            public Byte lfPitchAndFamily;

            [MarshalAs(UnmanagedType.ByValTStr, SizeConst = LF_FACESIZE)]
            public String lfFaceName;
        }

        [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
        public struct TEXTMETRIC
        {
            public Int32 tmHeight;
            public Int32 tmAscent;
            public Int32 tmDescent;
            public Int32 tmInternalLeading;
            public Int32 tmExternalLeading;
            public Int32 tmAveCharWidth;
            public Int32 tmMaxCharWidth;
            public Int32 tmWeight;
            public Int32 tmOverhang;
            public Int32 tmDigitizedAspectX;
            public Int32 tmDigitizedAspectY;
            public Char tmFirstChar;
            public Char tmLastChar;
            public Char tmDefaultChar;
            public Char tmBreakChar;
            public Byte tmItalic;
            public Byte tmUnderlined;
            public Byte tmStruckOut;
            public Byte tmPitchAndFamily;
            public Byte tmCharSet;
        }

        [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
        public struct ENUMLOGFONT
        {
            public LOGFONT elfLogFont;

            [MarshalAs(UnmanagedType.ByValTStr, SizeConst = LF_FULLFACESIZE)]
            public String elfFullName;

            [MarshalAs(UnmanagedType.ByValTStr, SizeConst = LF_FACESIZE)]
            public String elfStyle;
        }

        [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
        public struct NEWTEXTMETRIC
        {
            public Int32 tmHeight;
            public Int32 tmAscent;
            public Int32 tmDescent;
            public Int32 tmInternalLeading;
            public Int32 tmExternalLeading;
            public Int32 tmAveCharWidth;
            public Int32 tmMaxCharWidth;
            public Int32 tmWeight;
            public Int32 tmOverhang;
            public Int32 tmDigitizedAspectX;
            public Int32 tmDigitizedAspectY;
            public Char tmFirstChar;
            public Char tmLastChar;
            public Char tmDefaultChar;
            public Char tmBreakChar;
            public Byte tmItalic;
            public Byte tmUnderlined;
            public Byte tmStruckOut;
            public Byte tmPitchAndFamily;
            public Byte tmCharSet;
            public UInt32 ntmFlags;
            public UInt32 ntmSizeEM;
            public UInt32 ntmCellHeight;
            public UInt32 ntmAvgWidth;
        }

        public struct FontData
        {
            public ENUMLOGFONT LogFont;
            public NEWTEXTMETRIC TextMetric;
            public uint FontType;
        }

        [DllImport("gdi32.dll", CharSet = CharSet.Auto)]
        public extern static Int32 EnumFontFamiliesEx(IntPtr hdc, ref LOGFONT lpLogfont, FONTENUMPROC lpEnumFontFamExProc, IntPtr lParam, UInt32 dwFlags);

        public delegate Int32 FONTENUMPROC(ref ENUMLOGFONT lpelf, ref NEWTEXTMETRIC lpntm, UInt32 FontType, IntPtr lParam);
        public static int EnumFontFamExProc(ref ENUMLOGFONT lpelf, ref NEWTEXTMETRIC lpntm, uint FontType, IntPtr lParam)
        {
            allFontData.Add(new FontData() { LogFont = lpelf, TextMetric = lpntm, FontType = FontType });
            return 1;
        }

        #endregion

        private static List<FontData> allFontData;
        public static List<FontData> GetAllFonts()
        {
            allFontData = new List<FontData>();
            Graphics graphics = Graphics.FromHwnd(IntPtr.Zero);
            try
            {
                IntPtr hdc = graphics.GetHdc();
                var logfont = new LOGFONT() { lfCharSet = (byte)FontLanguageCharSet.DEFAULT_CHARSET };
                EnumFontFamiliesEx(hdc, ref logfont, new FONTENUMPROC(EnumFontFamExProc), IntPtr.Zero, 0);
            }
            catch (Exception)
            {
            }
            finally
            {
                graphics.ReleaseHdc();
            }

            return allFontData;
        }

    }
```

## Sample Code:
```cs
class Program
    {
        static void Main(string[] args)
        {
            List<GdiFonts.FontData> allFonts = GdiFonts.GetAllFonts();

            // Fixed Pitch & ANSI_CHARSET
            List<string> mono = (from f in allFonts where ((f.LogFont.elfLogFont.lfPitchAndFamily & 0x3) == (int)GdiFonts.FontPitch.FIXED_PITCH) & (GdiFonts.FontLanguageCharSet)f.LogFont.elfLogFont.lfCharSet == GdiFonts.FontLanguageCharSet.ANSI_CHARSET select f.LogFont.elfFullName).ToList<string>();

            // Variable Pitch & ANSI_CHARSET
            List<string> variable = (from f in allFonts where ((f.LogFont.elfLogFont.lfPitchAndFamily & 0x3) == (int)GdiFonts.FontPitch.VARIABLE_PITCH) & (GdiFonts.FontLanguageCharSet)f.LogFont.elfLogFont.lfCharSet == GdiFonts.FontLanguageCharSet.ANSI_CHARSET select f.LogFont.elfFullName).ToList<string>();
            Console.Read();
        }
    }
The EnumFontFamiliesEx API11/7/2015 6:20:13 AM - -94.230.89.241The LOGFONT structure defines the attributes of a font.11/3/2015 6:42:15 PM - -194.25.158.132
```
