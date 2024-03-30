
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError=true, CharSet=CharSet.Auto)]
static extern uint GetWindowModuleFileName(IntPtr hwnd,
   StringBuilder lpszFileName, uint cchFileNameMax);
```

## VB Signature:
```cs
<DllImport("user32.dll", SetLastError := True, CharSet := CharSet.Auto)> _
  Private Shared Function GetWindowModuleFileName(hwnd As IntPtr, _
    lpszFileName As StringBuilder, cchFileNameMax As UInteger) As UInteger
  End Function
```
