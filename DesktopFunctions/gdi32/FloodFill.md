
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern bool FloodFill(IntPtr hdc, int nXStart, int nYStart,
   uint crFill);
```

## VB Signature
```cs
Declare Function FloodFill Lib "gdi32" (ByVal hDC As Integer, ByVal x As Integer, ByVal y As Integer, ByVal crColor As Integer) As Integer
```
