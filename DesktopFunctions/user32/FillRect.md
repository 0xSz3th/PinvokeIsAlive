
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern int FillRect(IntPtr hDC, [In] ref RECT lprc, IntPtr hbr);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Private Shared Function FillRect(hDC As IntPtr, ByRef lprc As RECT, hbr As IntPtr) As Integer
End Function
```
