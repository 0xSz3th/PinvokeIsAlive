
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError = true)]
static extern bool DrawIconEx(IntPtr hdc, int xLeft, int yTop, IntPtr hIcon,
   int cxWidth, int cyHeight, int istepIfAniCur, IntPtr hbrFlickerFreeDraw,
   int diFlags);
```
