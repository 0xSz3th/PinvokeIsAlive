
## C# Signature:
```cs
[DllImport("user32.dll")]
public static extern DISP_CHANGE ChangeDisplaySettings(ref DEVMODE devMode, int flags);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Private Shared Function ChangeDisplaySettings(ByRef devMode As DEVMODE, ByVal flags As Integer) As DISP_CHANGE
End Function
```
