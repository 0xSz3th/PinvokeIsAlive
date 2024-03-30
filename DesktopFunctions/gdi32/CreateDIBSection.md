
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern IntPtr CreateDIBSection(IntPtr hdc, [In] ref BITMAPINFO pbmi,
   uint pila, out IntPtr ppvBits, IntPtr hSection, uint dwOffset);
```

## VB.NET Signature:
```cs
<DllImport("gdi32.dll")> _
  Private Shared Function CreateDIBSection(ByVal hdc As Int32, _
    ByRef pbmi As BITMAPINFO, ByVal iUsage As System.UInt32, _
    ByRef ppvBits As Int32, ByVal hSection As Int32, _
    ByVal dwOffset As System.UInt32) As Int32
  End Function
```
