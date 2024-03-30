
## C# Signature:
```cs
[DllImport("gdi32.dll",EntryPoint="GetTextExtentExPointW")]
static extern bool GetTextExtentExPoint(IntPtr hdc, [MarshalAs(UnmanagedType.LPWStr)] string lpszStr,
   int cchString, int nMaxExtent, out int lpnFit, int[] alpDx, out SIZE lpSize);
```
