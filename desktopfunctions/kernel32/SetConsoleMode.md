
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
static extern bool SetConsoleMode(IntPtr hConsoleHandle, uint dwMode);
```

## User-Defined Types (C#):
```cs
[Flags]
    private enum ConsoleModes : uint
    {
        ENABLE_PROCESSED_INPUT = 0x0001,
        ENABLE_LINE_INPUT = 0x0002,
        ENABLE_ECHO_INPUT = 0x0004,
        ENABLE_WINDOW_INPUT = 0x0008,
        ENABLE_MOUSE_INPUT = 0x0010,
        ENABLE_INSERT_MODE = 0x0020,
        ENABLE_QUICK_EDIT_MODE = 0x0040,
        ENABLE_EXTENDED_FLAGS = 0x0080,
        ENABLE_AUTO_POSITION = 0x0100,

        ENABLE_PROCESSED_OUTPUT = 0x0001,
        ENABLE_WRAP_AT_EOL_OUTPUT = 0x0002,
        ENABLE_VIRTUAL_TERMINAL_PROCESSING = 0x0004,
        DISABLE_NEWLINE_AUTO_RETURN = 0x0008,
        ENABLE_LVB_GRID_WORLDWIDE = 0x0010
    }
```

## User-Defined Types (C#):
```cs
[Flags]
    private enum ConsoleInputModes : uint
    {
        ENABLE_PROCESSED_INPUT = 0x0001,
        ENABLE_LINE_INPUT = 0x0002,
        ENABLE_ECHO_INPUT = 0x0004,
        ENABLE_WINDOW_INPUT = 0x0008,
        ENABLE_MOUSE_INPUT = 0x0010,
        ENABLE_INSERT_MODE = 0x0020,
        ENABLE_QUICK_EDIT_MODE = 0x0040,
        ENABLE_EXTENDED_FLAGS = 0x0080,
        ENABLE_AUTO_POSITION = 0x0100
    }

    [Flags]
    private enum ConsoleOutputModes : uint
    {
        ENABLE_PROCESSED_OUTPUT = 0x0001,
        ENABLE_WRAP_AT_EOL_OUTPUT = 0x0002,
        ENABLE_VIRTUAL_TERMINAL_PROCESSING = 0x0004,
        DISABLE_NEWLINE_AUTO_RETURN = 0x0008,
        ENABLE_LVB_GRID_WORLDWIDE = 0x0010
    }
```

## User-Defined Types (VB):
```cs
<Flags()> Public Enum ConsoleModes
    ' 55 /* Console Mode flags */
    ENABLE_PROCESSED_INPUT = &H1
    ENABLE_LINE_INPUT = &H2
    ENABLE_ECHO_INPUT = &H4
    ENABLE_WINDOW_INPUT = &H8
    ENABLE_MOUSE_INPUT = &H10
    ENABLE_INSERT_MODE = &H20
    ENABLE_QUICK_EDIT_MODE = &H40
    ENABLE_EXTENDED_FLAGS = &H80
    ENABLE_AUTO_POSITION = &H100

    ENABLE_PROCESSED_OUTPUT = &H1
    ENABLE_WRAP_AT_EOL_OUTPUT = &H2

  End Enum
```

## Sample Code:
```cs
IntPtr hOut = GetStdHandle(STD_OUTPUT_HANDLE);
        if (hOut != INVALID_HANDLE_VALUE)
        {
        uint mode;
        if (GetConsoleMode(hOut, out mode))
        {
            mode |= (uint)ConsoleOutputModes.ENABLE_VIRTUAL_TERMINAL_PROCESSING;
            SetConsoleMode(hOut, mode);
        }
        }
```
