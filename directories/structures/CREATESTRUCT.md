
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto)]
    public struct CREATESTRUCT
    {
        public IntPtr lpCreateParams;
        public IntPtr hInstance;
        public IntPtr hMenu;
        public IntPtr hwndParent;
        public int cy;
        public int cx;
        public int y;
        public int x;
        public int style;
        public IntPtr lpszName;
        public IntPtr lpszClass;
        public int dwExStyle;
    }
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Auto)> _
    Public Structure CREATESTRUCT
        Public lpCreateParams As IntPtr
        Public hInstance As IntPtr
        Public hMenu As IntPtr
        Public hwndParent As IntPtr
        Public cy As Integer
        Public cx As Integer
        Public y As Integer
        Public x As Integer
        Public style As Integer
        Public lpszName As IntPtr
        Public lpszClass As IntPtr
        Public dwExStyle As Integer
    End Structure
```
