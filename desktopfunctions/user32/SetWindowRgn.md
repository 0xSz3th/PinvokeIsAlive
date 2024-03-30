
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern int SetWindowRgn(IntPtr hWnd, IntPtr hRgn, bool bRedraw);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Public Function SetWindowRgn(ByVal hWnd As Long, ByVal hRgn As IntPtr, ByVal bRedraw As Boolean) As Long
End Function
```
