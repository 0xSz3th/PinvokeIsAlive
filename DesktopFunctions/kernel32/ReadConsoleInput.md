
## C# Signature:
```cs
[DllImport("kernel32.dll", CharSet = CharSet.Unicode, SetLastError = true, EntryPoint = "ReadConsoleInputW")]
static extern bool ReadConsoleInput(
        IntPtr hConsoleInput,
        [Out] INPUT_RECORD[] lpBuffer,
        uint nLength,
        out uint lpNumberOfEventsRead);
```

## C# Signature:
```cs
[DllImport("kernel32.dll", CharSet = CharSet.Unicode, SetLastError = true, EntryPoint = "ReadConsoleInputW")]
static extern bool ReadConsoleInput(
        IntPtr hConsoleInput,
        out INPUT_RECORD lpBuffer,
        uint nLength, // must be 1
        out uint lpNumberOfEventsRead);
```
