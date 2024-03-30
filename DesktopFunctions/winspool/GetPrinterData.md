
## C# Signature:
```cs
[DllImport("winspool.drv", CharSet=CharSet.Auto, SetLastError=true)]
static extern uint GetPrinterData(IntPtr hPrinter, string pValueName, out uint pType, byte[] pData, uint nSize, out uint pcbNeeded);
```
