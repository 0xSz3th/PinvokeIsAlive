
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError=true)]
static extern IntPtr CreateWindow(
       string lpClassName,
       string lpWindowName,
       uint dwStyle,
       int x,
       int y,
       int nWidth,
       int nHeight,
       IntPtr hWndParent,
       IntPtr hMenu,
       IntPtr hInstance,
       IntPtr lpParam);
```
