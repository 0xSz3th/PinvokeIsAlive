
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern bool ArcTo(IntPtr hdc, int nLeftRect, int nTopRect,
   int nRightRect, int nBottomRect, int nXRadial1, int nYRadial1,
   int nXRadial2, int nYRadial2);
```

## VB Signature:
```cs
Declare Function ArcTo Lib "gdi32.dll" (ByVal hdc As IntPtr, _
  ByVal nLeftRect As Integer, ByVal nTopRect As Integer, _
  ByVal nRightRect As Integer, ByVal nBottomRect As Integer, _
  ByVal nXRadial1 As Integer, ByVal nYRadial1 As Integer, _
  ByVal nXRadial2 As Integer, ByVal nYRadial2 As Integer) As Boolean
```
