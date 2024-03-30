
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
    static extern bool GetConsoleHistoryInfo(
        out CONSOLE_HISTORY_INFO ConsoleHistoryInfo
        );
```

## VB Signature:
```cs
Declare Function GetConsoleHistoryInfo Lib "kernel32.dll" (TODO) As TODO
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct CONSOLE_HISTORY_INFO
    {
        ushort cbSize;
        ushort HistoryBufferSize;
        ushort NumberOfHistoryBuffers;
        uint dwFlags;
    }
```
