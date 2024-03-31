
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
    struct IMAGELISTDRAWPARAMS 
    {
        public int cbSize;
        public IntPtr himl;
        public int i;
        public IntPtr hdcDst;
        public int x;
        public int y;
        public int cx;
        public int cy;
        public int xBitmap;
        public int yBitmap;
        public int rgbBk;
        public int rgbFg;
        public int fStyle;
        public int dwRop;
        public int fState;
        public int Frame;
        public int crEffect;                
    }
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _ 
    Public Structure IMAGELISTDRAWPARAMS
        Public cbSize As Integer
        Public himl As IntPtr
        Public i As Integer
        Public hdcDst As IntPtr
        Public x As Integer
        Public y As Integer
        Public cx As Integer
        Public cy As Integer
        Public xBitmap As Integer
        Public yBitmap As Integer
        Public rgbBk As Integer
        Public rgbFg As Integer
        Public fStyle As Integer
        Public dwRop As Integer
        Public fState As Integer
        Public Frame As Integer
        Public crEffect As Integer
    End Structure
```
