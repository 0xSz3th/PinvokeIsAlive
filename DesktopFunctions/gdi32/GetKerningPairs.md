
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern uint GetKerningPairs(IntPtr hdc, uint nNumPairs,
   [Out] KERNINGPAIR [] lpkrnpair);
```
