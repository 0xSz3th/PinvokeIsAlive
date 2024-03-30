
## C# Signature:
```cs
[DllImport("winspool.drv", EntryPoint="SetJobA")]
static extern int SetJobA(IntPtr hPrinter, int JobId,
   int Level, ref byte pJob, int Command_Renamed);
```

## VB Signature:
```cs
Declare Function SetJob Lib "winspool.drv" Alias "SetJobA" (hPrinter As IntPtr, JobId As Integer,
   Level As Integer, ByRef pJob As Byte, Command_Renamed As Integer)
```

## User-Defined Types:
```cs
Public Const JOB_CONTROL_PAUSE = &H1
    Public Const JOB_CONTROL_RESUME = &H2
    Public Const JOB_CONTROL_RESTART = &H4
    Public Const JOB_CONTROL_CANCEL = &H3
    Public Const JOB_CONTROL_DELETE = &H5
    Public Const JOB_CONTROL_RETAIN = &H8
    Public Const JOB_CONTROL_RELEASE = &H9
```

## Tips & Tricks:
```cs
int pHandle = 0;

PRINTER_DEFAULTS defaults = new PRINTER_DEFAULTS();

byte b = 0;

OpenPrinterA(printerName, ref pHandle, ref defaults);

SetJobA(pHandle, (int)jobID, 0, ref b, JOB_CONTROL_CANCEL);

ClosePrinter(pHandle);
```

## Sample Code:
```cs
dim Result as long = SetJob(handle, jobid, 0, Nothing, JOB_CONTROL_RESUME)
```
