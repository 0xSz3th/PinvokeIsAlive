
## C# Signature:
```cs
[DllImport("winspool.drv", CharSet=CharSet.Auto, SetLastError=true)]
static extern int GetPrinterDriver(IntPtr hPrinter, string pEnvironment, uint Level, IntPtr pDriverInfo, uint cbBuf, out uint pcbNeeded);
```
