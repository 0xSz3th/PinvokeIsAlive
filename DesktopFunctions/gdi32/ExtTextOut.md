
## C# Signature:
```cs
[DllImport("gdi32.dll", EntryPoint = "ExtTextOutW")]
static extern bool ExtTextOut(IntPtr hdc, int X, int Y, uint fuOptions,
   [In] ref RECT lprc, [MarshalAs(UnmanagedType.LPWStr)] string lpString, 
   uint cbCount, [In] IntPtr lpDx);
```

## C# Signature:
```cs
[Flags]
        public enum ETOOptions : uint
        {
            ETO_CLIPPED = 0x4,
            ETO_GLYPH_INDEX = 0x10,
            ETO_IGNORELANGUAGE = 0x1000,
            ETO_NUMERICSLATIN = 0x800,
            ETO_NUMERICSLOCAL = 0x400,
            ETO_OPAQUE = 0x2,
            ETO_PDY = 0x2000,
            ETO_RTLREADING = 0x800,
        }
```

## VB.NET Signature:
```cs
<DllImport("gdi32.dll")>
Public Function ExtTextOut(
        hdc As IntPtr,
        X As Integer,
        Y As Integer,
        fuOptions As UInteger,
        <[In]> ByRef lprc As RECT,
        <MarshalAs(UnmanagedType.LPWStr)> lpString As String,
        cbCount As UInteger,
        <[In]> lpDx As IntPtr) As Boolean
End Function
```
