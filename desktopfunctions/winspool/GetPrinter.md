
## C# Signature:
```cs
[DllImport("winspool.drv", EntryPoint = "GetPrinterA", SetLastError = true,
         CharSet = CharSet.Ansi, ExactSpelling = true,
         CallingConvention = CallingConvention.StdCall)]
    private static extern bool GetPrinter(IntPtr hPrinter, int dwLevel,
        IntPtr pPrinter, int dwBuf, out int dwNeeded);
```
