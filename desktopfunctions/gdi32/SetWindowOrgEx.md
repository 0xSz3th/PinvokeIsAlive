
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern bool SetWindowOrgEx(IntPtr hdc, int X, int Y, System.IntPtr lpPoint);
[DllImport("gdi32.dll")]
static extern bool SetWindowOrgEx(IntPtr hdc, int X, int Y, ref POINT lpPoint);
```
