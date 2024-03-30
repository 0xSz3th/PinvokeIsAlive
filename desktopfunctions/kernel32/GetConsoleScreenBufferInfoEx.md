
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

        // Hack Hack Hack
        // Too lazy to figure out the array at the moment...
        //public COLORREF[16] ColorTable;
        public COLORREF color0;
        public COLORREF color1;
        public COLORREF color2;
        public COLORREF color3;

        public COLORREF color4;
        public COLORREF color5;
        public COLORREF color6;
        public COLORREF color7;

        public COLORREF color8;
        public COLORREF color9;
        public COLORREF colorA;
        public COLORREF colorB;

        public COLORREF colorC;
        public COLORREF colorD;
        public COLORREF colorE;
        public COLORREF colorF;

        // has been a while since I did this, test before use
        // but should be something like:
        // 
        // [MarshalAs(UnmanagedType.ByValArray, SizeConst=16)]
        // public COLORREF[] ColorTable;
    }
```
