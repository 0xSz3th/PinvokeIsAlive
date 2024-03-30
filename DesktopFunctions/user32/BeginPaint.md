
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern IntPtr BeginPaint(IntPtr hwnd, out PAINTSTRUCT lpPaint);
```

## VB.Net Signature:
```cs
<DllImport("user32.dll")> _
Public Shared Function BeginPaint(ByVal hwnd As IntPtr, <Out()> ByRef lpPaint As PAINTSTRUCT) As IntPtr
End Function
```
