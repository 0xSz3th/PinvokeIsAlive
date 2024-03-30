
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern bool GetTextExtentExPointI(IntPtr hdc, ushort [] pgiIn,
   int cgi, int nMaxExtent, IntPtr lpnFit, IntPtr alpDx, out SIZE lpSize);
```
