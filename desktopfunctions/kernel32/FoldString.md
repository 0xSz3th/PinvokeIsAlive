
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool FoldString(uint dwMapFlags, string lpSrcStr, int cchSrc,
   [Out] StringBuilder lpDestStr, int cchDest);
```
