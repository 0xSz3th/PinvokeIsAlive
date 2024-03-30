
## C# Signature:
```cs
/* Copies a number of characters to consecutive cells of a console screen buffer,
        beginning at a specified location. */
    [DllImport("kernel32.dll", SetLastError = true)]
    internal static extern bool WriteConsoleOutputCharacter(
        IntPtr hConsoleOutput,
        StringBuilder lpCharacter,
        uint nLength,
        COORD dwWriteCoord,
        out uint lpNumberOfCharsWritten);
```
