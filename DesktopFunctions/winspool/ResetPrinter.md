
## C# Signature:
```cs
[DllImport("winspool.Drv", EntryPoint="ResetPrinterA", SetLastError=true, CharSet=CharSet.Ansi,ExactSpelling=true, CallingConvention=CallingConvention.StdCall)]
private static extern bool ResetPrinter(IntPtr hPrinter,ref PRINTER_DEFAULTS pd);
```

## VB Signature:
```cs
Declare Function ResetPrinter Lib "winspool.drv" (TODO) As TODO
```
