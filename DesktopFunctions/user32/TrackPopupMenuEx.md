
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool TrackPopupMenuEx(IntPtr hmenu, uint fuFlags, int x, int y,
   IntPtr hwnd, IntPtr lptpm);
```

## VB Signature:
```cs
<DllImport("User32.Dll")> _
    Shared Function TrackPopupMenuEx( _
    ByVal hmenu As IntPtr, ByVal fuFlags As UInt32, _
    ByVal x As Integer, ByVal y As Integer, _
    ByVal hwnd As IntPtr, ByVal lptpm As Integer) As Boolean
    End Function
```
