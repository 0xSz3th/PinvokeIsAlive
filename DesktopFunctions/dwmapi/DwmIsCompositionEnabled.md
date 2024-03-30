
## C# Signature:
```cs
[DllImport("dwmapi.dll")]
private static extern int DwmIsCompositionEnabled(out bool enabled);
```

## VB.NET Signature:
```cs
<DllImport("dwmapi.dll")> _
Private Shared Function DwmIsCompositionEnabled(ByRef enabled As Boolean) As Integer
End Function
```

## Notes:
```cs
Public Function AeroEnabled() As Boolean
     If Environment.OSVersion.Version.Major < 6 Then Return False
     Dim Enabled As Boolean
     DwmIsCompositionEnabled(Enabled)
     Return Enabled
End Function
```

## Notes:
```cs
Public Function AeroEnabled() As Boolean
     If Environment.OSVersion.Version.Major < 6 Then Return False
     DwmIsCompositionEnabled(AeroEnabled)
End Function
```

## If you're using DevExpress components::
```cs
DevExpress.Utils.Drawing.Helpers.NativeVista.IsCompositionEnabled();
```
