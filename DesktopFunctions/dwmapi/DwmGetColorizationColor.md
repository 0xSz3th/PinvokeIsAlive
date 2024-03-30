
## C# Signature:
```cs
[DllImport("dwmapi.dll", PreserveSig = false)]
static extern void DwmGetColorizationColor(out uint ColorizationColor, [MarshalAs(UnmanagedType.Bool)]out bool ColorizationOpaqueBlend);
```

## VB.NET Signature:
```cs
<DllImport("dwmapi.dll")> _
Private Shared Sub DwmGetColorizationColor(ByRef ColorizationColor As UInteger, ByRef ColorizationOpaqueBlend As Boolean)
End Sub
```
