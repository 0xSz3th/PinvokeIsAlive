
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool WriteConsoleOutputCharacter(IntPtr hConsoleOutput,
   string lpCharacter, uint nLength, COORD dwWriteCoord,
   out uint lpNumberOfCharsWritten);
```
