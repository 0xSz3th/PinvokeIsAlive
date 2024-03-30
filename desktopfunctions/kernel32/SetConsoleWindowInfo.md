
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
    static extern bool SetConsoleWindowInfo(
    IntPtr hConsoleOutput,
    bool bAbsolute,
    [In] ref SMALL_RECT lpConsoleWindow
    );
```

## VB Signature:
```cs
Declare Function SetConsoleWindowInfo Lib "kernel32.dll" (TODO) As TODO
```
