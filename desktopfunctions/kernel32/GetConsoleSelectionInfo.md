
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
    static extern bool GetConsoleSelectionInfo(
        CONSOLE_SELECTION_INFO ConsoleSelectionInfo
        );
```

## VB Signature:
```cs
Declare Function GetConsoleSelectionInfo Lib "kernel32.dll" (TODO) As TODO
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct CONSOLE_SELECTION_INFO 
    {
        uint Flags;
        COORD SelectionAnchor;
        SMALL_RECT Selection;

        // Flags values:
        const uint CONSOLE_MOUSE_DOWN = 0x0008; // Mouse is down
        const uint CONSOLE_MOUSE_SELECTION = 0x0004; //Selecting with the mouse
        const uint CONSOLE_NO_SELECTION = 0x0000; //No selection
        const uint CONSOLE_SELECTION_IN_PROGRESS = 0x0001; //Selection has begun
        const uint CONSOLE_SELECTION_NOT_EMPTY = 0x0002; //Selection rectangle is not empty
    }
```
