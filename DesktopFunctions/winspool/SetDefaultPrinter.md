
## C# Signature:
```cs
[DllImport("winspool.drv", CharSet=CharSet.Auto, SetLastError=true)]
    public static extern bool SetDefaultPrinter(string Name);
```

## VB Signature:
```cs
Declare Function SetDefaultPrinter Lib "winspool.drv" Alias "SetDefaultPrinterA" (ByVal pszPrinter As String) As Boolean
```

## Tips & Tricks:
```cs
{
    pinvokeResult = SendMessageTimeout(HWND_BROADCAST, WM_SETTINGCHANGE, IntPtr.Zero,
        IntPtr.Zero, SendMessageTimeoutFlags.SMTO_NORMAL, 1000, out innerPinvokeResult);
    }
```

## Sample Code:
```cs
// Locals
    bool result;
    IntPtr pinvokeResult;
    IntPtr HWND_BROADCAST;
    IntPtr innerPinvokeResult;

    // Set default printer
    result = SetDefaultPrinter(defaultPrinterName);

    // Notify running programs?
    if (result == true && notifyRunningPrograms == true)
    {
        // Tell all open programs that this change occurred.
        // Allow each program 1 second to handle this message.
        HWND_BROADCAST = new IntPtr(0xffff);
        pinvokeResult = SendMessageTimeout(HWND_BROADCAST, WM_SETTINGCHANGE, IntPtr.Zero,
            IntPtr.Zero, SendMessageTimeoutFlags.SMTO_NORMAL, 1000, out innerPinvokeResult);
    }

    // Return result
    return result;
```
