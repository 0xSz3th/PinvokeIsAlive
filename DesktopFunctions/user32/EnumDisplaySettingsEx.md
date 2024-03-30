
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool EnumDisplaySettingsEx(string lpszDeviceName, uint iModeNum, out DEVMODE lpDevMode, uint dwFlags);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Private Shared Function EnumDisplaySettingsEx(ByVal lpszDeviceName As String, ByVal iModeNum As UInteger, ByRef lpDevMode As DEVMODE, ByVal dwFlags As UInteger) As Boolean
End Function
```
