
## C# Signature:
```cs
[DllImport("winspool.drv")]
    static extern bool GetPrinterDriverDirectory(StringBuilder pName,
                              StringBuilder pEnv,
                              int Level, 
                              [Out] StringBuilder outPath,
                              int bufferSize,
                              ref int Bytes);
```

## VB Signature:
```cs
Declare Function GetPrinterDriverDir Lib "winspool.dll" (TODO) As TODO
```

## Sample Code:
```cs
private String GetPrinterDriverDir()
    {
        StringBuilder str = new StringBuilder(1024);
        int i = 0;
        GetPrinterDriverDirectory(null, null, 1, str, 1024, ref i);
        return str.ToString();
    }
```
