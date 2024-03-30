
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern IntPtr DefWindowProc(IntPtr hWnd, WindowsMessages uMsg, IntPtr wParam, IntPtr lParam);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Public Shared Function DefWindowProc(ByVal hWnd As IntPtr, ByVal uMsg As WindowsMessages, ByVal wParam As IntPtr, ByVal lParam As IntPtr) As IntPtr
End Function
```
