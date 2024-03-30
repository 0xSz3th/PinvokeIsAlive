
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern int DrawTextEx(IntPtr hdc, StringBuilder lpchText, int cchText,
   ref RECT lprc, uint dwDTFormat, ref DRAWTEXTPARAMS lpDTParams);
```
