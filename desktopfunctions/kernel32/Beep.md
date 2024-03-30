
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool Beep(uint dwFreq, uint dwDuration);
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll", SetLastError := True)> _
Private Shared Function Beep(dwFreq As UInteger, dwDuration As UInteger) As Boolean
End Function
```

## VB 6 Signature:
```cs
Declare Function Lib "kernel32.dll" Alias "Beep" (ByVal dwFrequency As Long, ByVal dwMilliseconds As Long) As Long
```

## VB.NET 10 Signature:
```cs
Public Declare Sub Wait Lib "kernel32" Alias "Sleep" (ByVal dwMilliseconds As Integer)
```

## Sample Code:
```cs
using System;
using System.Runtime.InteropServices;

class BeepSample
{
    [DllImport("kernel32.dll", SetLastError=true)]
    static extern bool Beep(uint dwFreq, uint dwDuration);

    static void Main()
    {
        Console.WriteLine("Testing PC speaker...");
        for (uint i = 100; i <= 20000; i++)
        {
            Beep(i, 5);
        }
        Console.WriteLine("Testing complete.");
    }
}
```
