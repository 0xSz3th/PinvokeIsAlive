
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern bool Chord(IntPtr hdc, int nLeftRect, int nTopRect,
   int nRightRect, int nBottomRect, int nXRadial1, int nYRadial1,
   int nXRadial2, int nYRadial2);
```

## VB.Net Signature:
```cs
<Runtime.InteropServices.DllImport("gdi32.dll")> _
Public Function Chord(ByVal hDc As IntPtr, ByVal nLeftRect As Integer, ByVal nTopRect As Integer,
               ByVal nRightRect As Integer, ByVal nBottomRect As Integer, ByVal nXRadial1 As Integer,
               ByVal nYRadial1 As Integer, ByVal nXRadial2 As Integer, ByVal nYRadial2 As Integer) As Boolean
End Function
```
