
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
    static extern bool SetConsoleScreenBufferInfoEx(
        IntPtr ConsoleOutput,
        ref CONSOLE_SCREEN_BUFFER_INFO_EX ConsoleScreenBufferInfoEx
        );
```

## VB Signature:
```cs
Declare Function SetConsoleScreenBufferInfoEx Lib "kernel32.dll" (TODO) As TODO
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
    }
```

## Sample Code:
```cs
// Copyright Alex Shvedov
// Modified by MercuryP with color specifications
// Use this code in any way you want

using System;
using System.Diagnostics;                // for Debug
using System.Drawing;                    // for Color (add reference to  System.Drawing assembly)
using System.Runtime.InteropServices;    // for StructLayout

internal class SetScreenColorsDemo
{
    [StructLayout(LayoutKind.Sequential)]
    internal struct COORD
    {
        internal short X;
        internal short Y;
    }
    [StructLayout(LayoutKind.Sequential)]
    internal struct SMALL_RECT
    {
        internal short Left;
        internal short Top;
        internal short Right;
        internal short Bottom;
    }
    [StructLayout(LayoutKind.Sequential)]
    internal struct COLORREF
    {
        internal uint ColorDWORD;

        internal COLORREF(Color color)
        {
            ColorDWORD = (uint)color.R + (((uint)color.G) << 8) + (((uint)color.B) << 16);
        }

        internal COLORREF(uint r, uint g, uint b)
        {
            ColorDWORD = r + (g << 8) + (b << 16);
        }

        internal Color GetColor()
        {
            return Color.FromArgb((int)(0x000000FFU & ColorDWORD),
               (int)(0x0000FF00U & ColorDWORD) >> 8, (int)(0x00FF0000U & ColorDWORD) >> 16);
        }

        internal void SetColor(Color color)
        {
            ColorDWORD = (uint)color.R + (((uint)color.G) << 8) + (((uint)color.B) << 16);
        }
    }
    [StructLayout(LayoutKind.Sequential)]
    internal struct CONSOLE_SCREEN_BUFFER_INFO_EX
    {
        internal int cbSize;
        internal COORD dwSize;
        internal COORD dwCursorPosition;
        internal ushort wAttributes;
        internal SMALL_RECT srWindow;
        internal COORD dwMaximumWindowSize;
        internal ushort wPopupAttributes;
        internal bool bFullscreenSupported;
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
    }

    const int STD_OUTPUT_HANDLE = -11;                                        // per WinBase.h
    internal static readonly IntPtr INVALID_HANDLE_VALUE = new IntPtr(-1);    // per WinBase.h

    [DllImport("kernel32.dll", SetLastError = true)]
    private static extern IntPtr GetStdHandle(int nStdHandle);

    [DllImport("kernel32.dll", SetLastError = true)]
    private static extern bool GetConsoleScreenBufferInfoEx(IntPtr hConsoleOutput, ref CONSOLE_SCREEN_BUFFER_INFO_EX csbe);

    [DllImport("kernel32.dll", SetLastError = true)]
    private static extern bool SetConsoleScreenBufferInfoEx(IntPtr hConsoleOutput, ref CONSOLE_SCREEN_BUFFER_INFO_EX csbe);

    /***            C prototype:
    #include <Windows.h>
    #include <stdio.h>
    //#include <conio.h>        // for _getch()

    int wmain() {
        CONSOLE_SCREEN_BUFFER_INFOEX info;
        info.cbSize = sizeof(info);
        HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);
        GetConsoleScreenBufferInfoEx(hConsole, &info);
        // info.ColorTable[0] - "Screen Background" color
        // info.ColorTable[7] - "Screen Text" color
        info.ColorTable[0] = RGB(0, 0, 200);
        info.ColorTable[7] = RGB(200, 200, 0);
        ++info.srWindow.Bottom;                    // reasons for these is unknown
        ++info.srWindow.Right;
        SetConsoleScreenBufferInfoEx(hConsole, &info);
        puts("Press ENTER to exit...");
        char bbb[100];
        gets_s(bbb);
        return 0;
    }
*/
```

## Sample Code:
```cs
// Set a specific console color to an RGB color
    // The default console colors used are gray (foreground) and black (background)
    public static int SetColor(ConsoleColor consoleColor, Color targetColor)
    {
        return SetColor(consoleColor, targetColor.R, targetColor.G, targetColor.B);
    }

    public static int SetColor(ConsoleColor color, uint r, uint g, uint b)
    {
        CONSOLE_SCREEN_BUFFER_INFO_EX csbe = new CONSOLE_SCREEN_BUFFER_INFO_EX();
        csbe.cbSize = (int)Marshal.SizeOf(csbe);                    // 96 = 0x60
        IntPtr hConsoleOutput = GetStdHandle(STD_OUTPUT_HANDLE);    // 7
        if (hConsoleOutput == INVALID_HANDLE_VALUE)
        {
            return Marshal.GetLastWin32Error();
        }
        bool brc = GetConsoleScreenBufferInfoEx(hConsoleOutput, ref csbe);
        if (!brc)
        {
            return Marshal.GetLastWin32Error();
        }

        switch (color)
        {
            case ConsoleColor.Black:
                csbe.black = new COLORREF(r, g, b);
                break;
            case ConsoleColor.DarkBlue:
                csbe.darkBlue = new COLORREF(r, g, b);
                break;
            case ConsoleColor.DarkGreen:
                csbe.darkGreen = new COLORREF(r, g, b);
                break;
            case ConsoleColor.DarkCyan:
                csbe.darkCyan = new COLORREF(r, g, b);
                break;
            case ConsoleColor.DarkRed:
                csbe.darkRed = new COLORREF(r, g, b);
                break;
            case ConsoleColor.DarkMagenta:
                csbe.darkMagenta = new COLORREF(r, g, b);
                break;
            case ConsoleColor.DarkYellow:
                csbe.darkYellow = new COLORREF(r, g, b);
                break;
            case ConsoleColor.Gray:
                csbe.gray = new COLORREF(r, g, b);
                break;
            case ConsoleColor.DarkGray:
                csbe.darkGray = new COLORREF(r, g, b);
                break;
            case ConsoleColor.Blue:
                csbe.blue = new COLORREF(r, g, b);
                break;
            case ConsoleColor.Green:
                csbe.green = new COLORREF(r, g, b);
                break;
            case ConsoleColor.Cyan:
                csbe.cyan = new COLORREF(r, g, b);
                break;
            case ConsoleColor.Red:
                csbe.red = new COLORREF(r, g, b);
                break;
            case ConsoleColor.Magenta:
                csbe.magenta = new COLORREF(r, g, b);
                break;
            case ConsoleColor.Yellow:
                csbe.yellow = new COLORREF(r, g, b);
                break;
            case ConsoleColor.White:
                csbe.white = new COLORREF(r, g, b);
                break;
        }
        ++csbe.srWindow.Bottom;
        ++csbe.srWindow.Right;
        brc = SetConsoleScreenBufferInfoEx(hConsoleOutput, ref csbe);
        if (!brc)
        {
            return Marshal.GetLastWin32Error();
        }
        return 0;
    }

    public static int SetScreenColors(Color foregroundColor, Color backgroundColor)
    {
        int irc;
        irc = SetColor(ConsoleColor.Gray, foregroundColor);
        if (irc != 0) return irc;
        irc = SetColor(ConsoleColor.Black, backgroundColor);
        if (irc != 0) return irc;

        return 0;
    }

    private static void Main(string[] args)
    {
        Color screenTextColor = Color.Red;
        Color screenBackgroundColor = Color.Blue;
        int irc = SetScreenColors(screenTextColor, screenBackgroundColor);
        Debug.Assert(irc == 0, "SetScreenColors failed, Win32Error code = " + irc + " = 0x" + irc.ToString("x"));

        Debug.WriteLine("LargestWindowHeight=" + Console.LargestWindowHeight + " LargestWindowWidth=" + Console.LargestWindowWidth);
        Debug.WriteLine("BufferHeight=" + Console.BufferHeight + " WindowHeight=" + Console.WindowHeight + " BufferWidth=" + Console.BufferWidth + " WindowWidth=" + Console.WindowWidth);
        //// these are relative to the buffer, not the screen:
        //Debug.WriteLine("WindowTop=" + Console.WindowTop + " WindowLeft=" + Console.WindowLeft);
        Debug.WriteLine("ForegroundColor=" + Console.ForegroundColor + " BackgroundColor=" + Console.BackgroundColor);
        Console.WriteLine("Some text in a console window");
        Console.BackgroundColor = ConsoleColor.Cyan;
        Console.ForegroundColor = ConsoleColor.Yellow;
        Debug.WriteLine("ForegroundColor=" + Console.ForegroundColor + " BackgroundColor=" + Console.BackgroundColor);
        Console.Write("Press ENTER to exit...");
        Console.ReadLine();

        // Note: If you use SetScreenColors, the RGB values of gray and black are changed permanently for the console window.
        // Using i.e. Console.ForegroundColor = ConsoleColor.Gray afterwards will switch the color to whatever you changed gray to

        // It's best to use SetColor for the purpose of choosing the 16 colors you want the console to be able to display, then use
        // Console.BackgroundColor and Console.ForegrondColor to choose among them.
    }
}
```
