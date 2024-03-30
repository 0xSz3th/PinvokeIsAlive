
## C# Signature:
```cs
[DllImport("kernel32.dll", CharSet = CharSet.Unicode, SetLastError = true)]
    extern static bool GetCurrentConsoleFontEx(
    IntPtr hConsoleOutput,
    bool bMaximumWindow, 
    ref CONSOLE_FONT_INFOEX lpConsoleCurrentFont);
```

## VB Signature:
```cs
Declare Function GetCurrentConsoleFontEx Lib "kernel32.dll" (TODO) As TODO
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
    private struct COORD
    {
        public short X;
        public short Y;

        public COORD(short x, short y)
        {
        X = x;
        Y = y;
        }
    }

    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
    private struct CONSOLE_FONT_INFOEX
    {
        public uint cbSize;
        public uint nFont;
        public COORD dwFontSize;
        public int FontFamily;
        public int FontWeight;

        [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 32)]
        public string FaceName;
    }
```

## Sample Code:
```cs
using System.Runtime.InteropServices;
using System;

namespace Win32test
{
    class ConsoleTest
    {
    [DllImport("kernel32.dll", CharSet = CharSet.Unicode, SetLastError = true)]
    extern static bool GetCurrentConsoleFontEx(
        IntPtr hConsoleOutput,
        bool bMaximumWindow,
        ref CONSOLE_FONT_INFOEX lpConsoleCurrentFont);

    private enum StdHandle
    {
        OutputHandle = -11
    }

    [DllImport("kernel32")]
    private static extern IntPtr GetStdHandle(StdHandle index);

    static void Main(string[] args)
    {
        // Instantiating CONSOLE_FONT_INFOEX and setting cbsize
        CONSOLE_FONT_INFOEX ConsoleFontInfo = new CONSOLE_FONT_INFOEX();
        ConsoleFontInfo.cbSize = (uint)Marshal.SizeOf(ConsoleFontInfo);

        GetCurrentConsoleFontEx(GetStdHandle(StdHandle.OutputHandle), false, ref ConsoleFontInfo);

        // Printing the results
        Console.WriteLine($"Font size is: x: {ConsoleFontInfo.dwFontSize.X} y: {ConsoleFontInfo.dwFontSize.Y}");
        Console.WriteLine($"Font name is: {ConsoleFontInfo.FaceName}");
        Console.WriteLine($"Fontfamily is: {ConsoleFontInfo.FontFamily}");
        Console.WriteLine($"Fontweight is: {ConsoleFontInfo.FontWeight}");
        Console.WriteLine($"Font index is: {ConsoleFontInfo.nFont}");
        Console.ReadKey();
    }

    [StructLayout(LayoutKind.Sequential)]
    private struct COORD
    {
        public short X;
        public short Y;

        public COORD(short x, short y)
        {
        X = x;
        Y = y;
        }
    }

    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
    private struct CONSOLE_FONT_INFOEX
    {
        public uint cbSize;
        public uint nFont;
        public COORD dwFontSize;
        public int FontFamily;
        public int FontWeight;

        [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 32)]
        public string FaceName;
    }
    }
}
```
