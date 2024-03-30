
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true)]
static extern int SetConsoleFont(IntPtr hOut, uint dwFontSize);
```

## VB Signature:
```cs
Declare Function SetConsoleFont Lib "kernel32.dll" (hOut As IntPtr, dwFontSize As UInt32) As Integer
```

## Sample Code:
```cs
const int STD_OUT_HANDLE = -11;

    [DllImport("kernel32.dll", SetLastError = true)]
    static extern int SetConsoleFont(
        IntPtr hOut, 
        uint dwFontNum
        );

    [DllImport("kernel32.dll", SetLastError = true)]
    static extern IntPtr GetStdHandle(int dwType);

    Console.WriteLine("This is an error!");
    Console.ReadLine();
    SetConsoleFont(GetStdHandle(STD_OUT_HANDLE), 9);
    Console.ReadLine();
```
