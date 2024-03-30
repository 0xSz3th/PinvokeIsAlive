
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
    static extern bool GetConsoleScreenBufferInfoEx(
        IntPtr hConsoleOutput,
        ref CONSOLE_SCREEN_BUFFER_INFO_EX ConsoleScreenBufferInfo
        );
```

## VB Signature:
```cs
Declare Function GetConsoleScreenBufferInfoEx Lib "kernel32.dll" (TODO) As TODO
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct CONSOLE_SCREEN_BUFFER_INFO_EX
    {
        public uint cbSize;
        public COORD dwSize;
        public COORD dwCursorPosition;
        public short wAttributes;
        public SMALL_RECT srWindow;
        public COORD dwMaximumWindowSize;

        public ushort wPopupAttributes;
        public bool bFullscreenSupported;
```

## User-Defined Types:
```cs
internal COLORREF black;
        internal COLORREF darkBlue;
        internal COLORREF darkGreen;
        internal COLORREF darkCyan;
        internal COLORREF darkRed;
        internal COLORREF darkMagenta;
        internal COLORREF darkYellow;
        internal COLORREF gray;
        internal COLORREF darkGray;
        internal COLORREF blue;
        internal COLORREF green;
        internal COLORREF cyan;
        internal COLORREF red;
        internal COLORREF magenta;
        internal COLORREF yellow;
        internal COLORREF white;

        // has been a while since I did this, test before use
        // but should be something like:
        // 
        // [MarshalAs(UnmanagedType.ByValArray, SizeConst=16)]
        // public COLORREF[] ColorTable;
    }
```
