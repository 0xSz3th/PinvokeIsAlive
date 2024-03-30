
## C# Definition:
```cs
[StructLayout(LayoutKind.Explicit, CharSet = CharSet.Ansi)]
struct DEVMODE
{
    public const int CCHDEVICENAME = 32;
    public const int CCHFORMNAME = 32;

    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = CCHDEVICENAME)]
    [System.Runtime.InteropServices.FieldOffset(0)]
    public string dmDeviceName;
    [System.Runtime.InteropServices.FieldOffset(32)]
    public Int16 dmSpecVersion;
    [System.Runtime.InteropServices.FieldOffset(34)]
    public Int16 dmDriverVersion;
    [System.Runtime.InteropServices.FieldOffset(36)]
    public Int16 dmSize;
    [System.Runtime.InteropServices.FieldOffset(38)]
    public Int16 dmDriverExtra;
    [System.Runtime.InteropServices.FieldOffset(40)]
    public DM dmFields;

    [System.Runtime.InteropServices.FieldOffset(44)]
    Int16 dmOrientation;
    [System.Runtime.InteropServices.FieldOffset(46)]
    Int16 dmPaperSize;
    [System.Runtime.InteropServices.FieldOffset(48)]
    Int16 dmPaperLength;
    [System.Runtime.InteropServices.FieldOffset(50)]
    Int16 dmPaperWidth;
    [System.Runtime.InteropServices.FieldOffset(52)]
    Int16 dmScale;
    [System.Runtime.InteropServices.FieldOffset(54)]
    Int16 dmCopies;
    [System.Runtime.InteropServices.FieldOffset(56)]
    Int16 dmDefaultSource;
    [System.Runtime.InteropServices.FieldOffset(58)]
    Int16 dmPrintQuality;

    [System.Runtime.InteropServices.FieldOffset(44)]
    public POINTL dmPosition;
    [System.Runtime.InteropServices.FieldOffset(52)]
    public Int32 dmDisplayOrientation;
    [System.Runtime.InteropServices.FieldOffset(56)]
    public Int32 dmDisplayFixedOutput;

    [System.Runtime.InteropServices.FieldOffset(60)]
    public short dmColor; // See note below!
    [System.Runtime.InteropServices.FieldOffset(62)]
    public short dmDuplex; // See note below!
    [System.Runtime.InteropServices.FieldOffset(64)]
    public short dmYResolution;
    [System.Runtime.InteropServices.FieldOffset(66)]
    public short dmTTOption;
    [System.Runtime.InteropServices.FieldOffset(68)]
    public short dmCollate; // See note below!
    [System.Runtime.InteropServices.FieldOffset(70)]
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = CCHFORMNAME)]
    public string dmFormName;
    [System.Runtime.InteropServices.FieldOffset(102)]
    public Int16 dmLogPixels;
    [System.Runtime.InteropServices.FieldOffset(104)]
    public Int32 dmBitsPerPel;
    [System.Runtime.InteropServices.FieldOffset(108)]
    public Int32 dmPelsWidth;
    [System.Runtime.InteropServices.FieldOffset(112)]
    public Int32 dmPelsHeight;
    [System.Runtime.InteropServices.FieldOffset(116)]
    public Int32 dmDisplayFlags;
    [System.Runtime.InteropServices.FieldOffset(116)]
    public Int32 dmNup;
    [System.Runtime.InteropServices.FieldOffset(120)]
    public Int32 dmDisplayFrequency;
}
```

## VB.NET Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _
Public Structure DEVMODE
    Public Const CCHDEVICENAME As Integer = 32
    Public Const CCHFORMNAME As Integer = 32

    <MarshalAs(UnmanagedType.ByValTStr, SizeConst := CCHDEVICENAME)> _
    Public dmDeviceName As String
    Public dmSpecVersion As Short
    Public dmDriverVersion As Short
    Public dmSize As Short
    Public dmDriverExtra As Short
    Public dmFields As DM

    Public dmOrientation As Short
    Public dmPaperSize As Short
    Public dmPaperLength As Short
    Public dmPaperWidth As Short

    Public dmScale As Short
    Public dmCopies As Short
    Public dmDefaultSource As Short
    Public dmPrintQuality As Short
    Public dmColor As Short
    Public dmDuplex As Short
    Public dmYResolution As Short
    Public dmTTOption As Short
    Public dmCollate As Short
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst := CCHFORMNAME)> _
    Public dmFormName As String
    Public dmLogPixels As Short
    Public dmBitsPerPel As Integer ' Declared wrong in the full framework
    Public dmPelsWidth As Integer
    Public dmPelsHeight As Integer
    Public dmDisplayFlags As Integer
    Public dmDisplayFrequency As Integer

    Public dmICMMethod As Integer
    Public dmICMIntent As Integer
    Public dmMediaType As Integer
    Public dmDitherType As Integer
    Public dmReserved1 As Integer
    Public dmReserved2 As Integer
    Public dmPanningWidth As Integer
    Public dmPanningHeight As Integer

    Public dmPositionX As Integer ' Using a PointL Struct does not work
    Public dmPositionY As Integer 
End Structure
```

## VB.NET Definition:
```cs
struct POINTL
{
    public Int32 x; 
    public Int32 y;
}
```

## Notes:
```cs
using System.Runtime.InteropServices;
```

## Notes:
```cs
Imports System.Runtime.InteropServices
```

## Tips & Tricks:
```cs
DEVMODE d = new DEVMODE();
d.dmSize = Marshal.SizeOf(typeof(DEVMODE));
```

## Tips & Tricks:
```cs
public short dmColor;
public short dmDuplex;
public short dmCollate;
```

## Tips & Tricks:
```cs
public DMCOLOR dmColor;
public DMDUP dmDuplex;
public DMCOLLATE dmCollate;
```

## Tips & Tricks:
```cs
[StructLayout(LayoutKind.Sequential, Pack = 1, CharSet = CharSet.Auto)]
    internal struct DM_DOTNET
    {
    private const int CCHDEVICENAME2 = 32;
    private const int CCHFORMNAME2 = 32;

    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = CCHDEVICENAME2)]
    public string dmDeviceName;
    public Int16 dmSpecVersion;
    public Int16 dmDriverVersion;
    public Int16 dmSize;
    public Int16 dmDriverExtra;
    public DM dmFields;

    public Int16 dmOrientation;
    public Int16 dmPaperSize;
    public Int16 dmPaperLength;
    public Int16 dmPaperWidth;
    public Int16 dmScale;
    public Int16 dmCopies;
    public Int16 dmDefaultSource;
    public Int16 dmPrintQuality;

    public POINTL dmPosition;
    public Int32 dmDisplayOrientation;
    public Int32 dmDisplayFixedOutput;

    public short dmColor;
    public short dmDuplex; 
    public short dmYResolution;
    public short dmTTOption;
    public short dmCollate;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = CCHFORMNAME2)]
    public string dmFormName;
    public Int16 dmLogPixels;
    public Int32 dmBitsPerPel;
    public Int32 dmPelsWidth;
    public Int32 dmPelsHeight;
    public Int32 dmDisplayFlags;    
    //public Int32 dmNup;
    public Int32 dmDisplayFrequency;
    }
```

## Tips & Tricks:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi)]
    private struct DEVMODE
    {
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 32)]
    public string dmDeviceName;
    public short dmSpecVersion;
    public short dmDriverVersion;
    public short dmSize;
    public short dmDriverExtra;
    public int dmFields;
    public short dmOrientation;
    public short dmPaperSize;
    public short dmPaperLength;
    public short dmPaperWidth;
    public short dmScale;
    public short dmCopies;
    public short dmDefaultSource;
    public short dmPrintQuality;
    public short dmColor;
    public short dmDuplex;
    public short dmYResolution;
    public short dmTTOption;
    public short dmCollate;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 32)]
    public string dmFormName;
    public short dmUnusedPadding;
    public short dmBitsPerPel;
    public int dmPelsWidth;
    public int dmPelsHeight;
    public int dmDisplayFlags;
    public int dmDisplayFrequency;
    }
```

## Sample Code:
```cs
[DllImport("kernel32.dll", ExactSpelling = true)]
  public static extern IntPtr GlobalSize(IntPtr handle);
```

## Sample Code:
```cs
devMode = (DEVMODE)Marshal.PtrToStructure(pDevMode, typeof(DEVMODE));
  devMode.dmSize = (short)Marshal.SizeOf(devMode);
  int isize = GlobalSize(hDevMode).ToInt32() - (int)devMode.dmSize;
  devMode.dmDriverExtra = Convert.ToInt16(isize);
```
