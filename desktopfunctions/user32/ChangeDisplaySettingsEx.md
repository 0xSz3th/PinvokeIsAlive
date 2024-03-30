
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern DISP_CHANGE ChangeDisplaySettingsEx(string lpszDeviceName, ref DEVMODE lpDevMode, IntPtr hwnd, ChangeDisplaySettingsFlags dwflags, IntPtr lParam);
```

## VB.NET
```cs
<DllImport("user32.dll")> _
Private Shared Function ChangeDisplaySettingsEx(ByVal lpszDeviceName As String, ByRef lpDevMode As DEVMODE, ByVal hwnd As IntPtr, ByVal dwflags As UInteger, ByVal lParam As IntPtr) As DISP_CHANGE
End Function
```

## Sample Code:
```cs
DISPLAY_DEVICE d = new DISPLAY_DEVICE();
DEVMODE dm = new DEVMODE(); 
d.cb = Marshal.SizeOf(d);
int deviceID=1; // This is only for my device setting. Go through the whole EnumDisplayDevices to find your device  
EnumDisplayDevices(null,deviceID, ref  d, 0); // 
EnumDisplaySettings(d.DeviceName, 0, ref dm);
dm.dmPelsWidth = 1024;
dm.dmPelsHeight = 768;
dm.dmPositionX = Screen.PrimaryScreen.Bounds.Right;
dm.dmFields = DM.Position | DM.PelsWidth | DM.PelsHeight;
ChangeDisplaySettingsEx(d.DeviceName, ref dm, IntPtr.Zero, CDS_UPDATEREGISTRY, IntPtr.Zero);
```
