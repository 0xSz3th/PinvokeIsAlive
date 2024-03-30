
## C# Signature:
```cs
[DllImport("kernel32.dll", CharSet = CharSet.Unicode, SetLastError = true)]
    extern static bool GetCurrentConsoleFontEx(IntPtr hConsoleOutput, bool bMaximumWindow, [In, Out] CONSOLE_FONT_INFOEX lpConsoleCurrentFont);
```

## VB Signature:
```cs
Declare Function GetCurrentConsoleFontEx Lib "kernel32.dll" (TODO) As TODO
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
    public class CONSOLE_FONT_INFO_EX
    {
    private int cbSize;
    public CONSOLE_FONT_INFO_EX()
    {
        cbSize = Marshal.SizeOf(typeof(CONSOLE_FONT_INFO_EX));
    }
    public int FontIndex;
    public short FontWidth;
    public short FontHeight;
    public int FontFamily;
    public int FontWeight;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 32)]
    public string FaceName;
    }
```
