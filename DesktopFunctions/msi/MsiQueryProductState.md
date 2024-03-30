
## C# Signature:
```cs
[DllImport("msi.dll", SetLastError=true)]
static extern INSTALLSTATE MsiQueryProductState(string product);
```

## VB Signature:
```cs
Declare Function MsiQueryProductState Lib "msi.dll" (ByVal product As String) As INSTALLSTATE
```

## Sample Code:
```cs
using System;
using System.Runtime.InteropServices;

public class QueryProductState
{
    [DllImport("msi.dll")]
    private static extern INSTALLSTATE MsiQueryProductState(string product); 

    public static void Main(string[] args)
    {
        INSTALLSTATE state = MsiQueryProductState("{11111111-2222-3333-4444-555555555555}");

        Console.WriteLine(state);
    }
}
```
