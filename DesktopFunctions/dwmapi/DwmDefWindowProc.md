
## C# Signature:
```cs
[DllImport("dwmapi.dll")]
static extern bool DwmDefWindowProc(IntPtr hWnd, int msg, IntPtr wParam, IntPtr lParam, ref IntPtr plResult);
```

## VB.NET Signature:
```cs
<DllImport("dwmapi.dll")> _
Private Shared Function DwmDefWindowProc(ByVal hWnd As IntPtr, ByVal msg As Integer, ByVal wParam As IntPtr, ByVal lParam As IntPtr, ByRef plResult As IntPtr) As Integer
End Function
```
