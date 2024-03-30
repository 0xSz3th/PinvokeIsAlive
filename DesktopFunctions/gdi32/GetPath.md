
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern int GetPath(IntPtr hdc, [Out] POINT [] lpPoints,
   [Out] byte [] lpTypes, int nSize);
```
