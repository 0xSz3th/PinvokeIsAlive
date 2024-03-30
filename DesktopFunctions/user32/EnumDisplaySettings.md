
## C# Signature:
```cs
[DllImport("user32.dll")]
public static extern bool EnumDisplaySettings (string deviceName, int modeNum, ref DEVMODE devMode );
```

## VB.NET Signature:
```cs
<DllImport("user32")> _
Public Function EnumDisplaySettings(ByVal deviceName As String, ByVal modeNum As Integer, ByRef devMode As DEVMODE) As Boolean
End Function
```

## Notes:
```cs
const int ENUM_CURRENT_SETTINGS = -1;
const int ENUM_REGISTRY_SETTINGS = -2;
```

## Sample Code:
```cs
using System.Runtime.InteropServices;
[StructLayout(LayoutKind.Sequential)]
public struct DEVMODE
{
    private const int CCHDEVICENAME = 0x20;
    private const int CCHFORMNAME = 0x20;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 0x20)]
    public string dmDeviceName;
    public short dmSpecVersion;
    public short dmDriverVersion;
    public short dmSize;
    public short dmDriverExtra;
    public int dmFields;
    public int dmPositionX;
    public int dmPositionY;
    public ScreenOrientation dmDisplayOrientation;
    public int dmDisplayFixedOutput;
    public short dmColor;
    public short dmDuplex;
    public short dmYResolution;
    public short dmTTOption;
    public short dmCollate;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 0x20)]
    public string dmFormName;
    public short dmLogPixels;
    public int dmBitsPerPel;
    public int dmPelsWidth;
    public int dmPelsHeight;
    public int dmDisplayFlags;
    public int dmDisplayFrequency;
    public int dmICMMethod;
    public int dmICMIntent;
    public int dmMediaType;
    public int dmDitherType;
    public int dmReserved1;
    public int dmReserved2;
    public int dmPanningWidth;
    public int dmPanningHeight;
}

[DllImport("user32.dll")]
public static extern bool EnumDisplaySettings(string lpszDeviceName, int iModeNum, ref DEVMODE lpDevMode);

private void button1_Click(object sender, EventArgs e)
{   
    DEVMODE vDevMode = new DEVMODE();
    int i = 0;
    while (EnumDisplaySettings(null, i, ref vDevMode))
    {
    Console.WriteLine("Width:{0} Height:{1} Color:{2} Frequency:{3}", 
        vDevMode.dmPelsWidth,
        vDevMode.dmPelsHeight,
    1 << vDevMode.dmBitsPerPel,
        vDevMode.dmDisplayFrequency
    );
    i++;
    }
}
```
