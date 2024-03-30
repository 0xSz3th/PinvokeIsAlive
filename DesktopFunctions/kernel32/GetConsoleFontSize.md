
## C# Signature:
```cs
[DllImport("kernel32.dll")]
    static extern Coord GetConsoleFontSize(
        IntPtr hConsoleOutput,
        Int32 nFont);
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct Coord
    {
        public short X;
        public short Y;
    }
```

## Sample Code:
```cs
private Coord GetCurrentFontSize()
    {

      //Need to use reflection to obtain pointer to the console output buffer
      Type consoleType = typeof(Console);

      IntPtr _consoleOutputHandle = (IntPtr)consoleType.InvokeMember(
        "_consoleOutputHandle",
        BindingFlags.Static | BindingFlags.NonPublic | BindingFlags.GetField,
        null,
        null,
        null);

       //Obtain the current console font index
        CONSOLE_FONT_INFO currentFont;
        bool success = GetCurrentConsoleFont(
        _consoleOutputHandle,
        false,
        out currentFont);

       //Use that index to obtain font size    
        Coord coord = GetConsoleFontSize(_consoleOutputHandle, currentFont.nFont);
        return coord;
    }
```
