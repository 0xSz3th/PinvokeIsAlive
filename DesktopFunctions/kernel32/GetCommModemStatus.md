
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool GetCommModemStatus(SafeFileHandle hFile, out uint lpModemStat);
```

## Sample Code:
```cs
const uint MS_CTS_ON = 16;
    uint LastCtsStat;

    // watching for CTS (Clear To Send)
    void watchdog_Tick(object sender, EventArgs e)
    {
        if (!hComPort.IsInvalid)
        {
        uint stat;
        GetCommModemStatus(hComPort, out stat);

        if (stat == MS_CTS_ON)
        {
            if (LastCtsStat == 0)
            {
            LastCtsStat = 1;
            CTSEvent(true);    // invoke event handler
            }
        }
        else
        {
            if (LastCtsStat >= 1)
            {
            LastCtsStat = 0;
            CTSEvent(false);
            }
        }
        }
    }
```
