
## C# Signature:
```cs
[DllImport("winspool.Drv", EntryPoint = "DocumentPropertiesW", SetLastError = true, ExactSpelling = true, CallingConvention = CallingConvention.StdCall)]
static extern int DocumentProperties(IntPtr hwnd, IntPtr hPrinter, [MarshalAs(UnmanagedType.LPWStr)] string pDeviceName, IntPtr pDevModeOutput, IntPtr pDevModeInput, int fMode);

[DllImport("winspool.drv", CharSet = CharSet.Unicode, SetLastError = true)]
static extern int DocumentProperties(IntPtr hWnd, IntPtr hPrinter, string pDeviceName, IntPtr pDevModeOutput, IntPtr pDevModeInput, fModes fMode);
```

## VB Signature:
```cs
<DllImport("winspool.Drv", EntryPoint:="DocumentPropertiesW", SetLastError:=True, ExactSpelling:=True, CallingConvention:=CallingConvention.StdCall)> _
    Private Shared Function DocumentProperties(ByVal hwnd As IntPtr, ByVal hPrinter As IntPtr, <MarshalAs(UnmanagedType.LPWStr)> ByVal pDeviceName As String, ByVal pDevModeOutput As IntPtr, ByVal pDevModeInput As IntPtr, ByVal fMode As Integer) As Integer
    End Function
```

## Sample Code:
```cs
public IntPtr GetDevMode(IntPtr printerHandle, string printerName)
{
   int sizeNeeded = DocumentProperties(IntPtr.Zero, printerHandle, printerName, IntPtr.Zero, IntPtr.Zero, fModes.DM_SIZEOF);
   if (sizeNeeded < 0)
   {
     throw new Win32Exception(Marshal.GetLastWin32Error());
   }

   // not really required, but see example: http://support.microsoft.com/kb/828638/en-us
   sizeNeeded += 100;

   IntPtr pdevmode = Marshal.AllocHGlobal(sizeNeeded);

   int result = DocumentProperties(IntPtr.Zero, printerHandle, printerName, pdevmode, IntPtr.Zero, fModes.DM_OUT_BUFFER);
   if (result < 0)
   {
     throw new Win32Exception(Marshal.GetLastWin32Error());
   }

   return pdevmode;
}
```

## Sample Code:
```cs
Marshal.FreeHGlobal(IntPtr);
```

## Sample Code:
```cs
private void OpenPrinterPropertiesDialog(PrinterSettings printerSettings)
    {
        IntPtr hDevMode = printerSettings.GetHdevmode(printerSettings.DefaultPageSettings);
        IntPtr pDevMode = GlobalLock(hDevMode);
        int sizeNeeded = DocumentProperties(this.Handle, IntPtr.Zero, printerSettings.PrinterName, pDevMode, pDevMode, 0);
        IntPtr devModeData = Marshal.AllocHGlobal(sizeNeeded);
        DocumentProperties(this.Handle, IntPtr.Zero, printerSettings.PrinterName, devModeData, pDevMode, 14);
        GlobalUnlock(hDevMode);
        printerSettings.SetHdevmode(devModeData);
        printerSettings.DefaultPageSettings.SetHdevmode(devModeData);
        GlobalFree(hDevMode);
        Marshal.FreeHGlobal(devModeData);
    }
```

## Sample Code:
```cs
private void OpenPrinterPropertiesDialog(PrinterSettings printerSettings)
    {
        IntPtr hDevMode = printerSettings.GetHdevmode(printerSettings.DefaultPageSettings);
        IntPtr pDevMode = GlobalLock(hDevMode);
        int sizeNeeded = DocumentProperties(this.Handle, IntPtr.Zero, printerSettings.PrinterName, pDevMode, pDevMode, 0);
        IntPtr devModeData = Marshal.AllocHGlobal(sizeNeeded);
        DocumentProperties(this.Handle, IntPtr.Zero, printerSettings.PrinterName, IntPtr.Zero, pDevMode, 14);
        GlobalUnlock(hDevMode);
        printerSettings.SetHdevmode(devModeData);
        printerSettings.DefaultPageSettings.SetHdevmode(devModeData);
        GlobalFree(hDevMode);
        Marshal.FreeHGlobal(devModeData);
    }
```

## Sample Code:
```cs
private void OpenPrinterPropertiesDialog(PrinterSettings printerSettings)
    {
        IntPtr hDevMode = printerSettings.GetHdevmode(printerSettings.DefaultPageSettings);
        IntPtr pDevMode = GlobalLock(hDevMode);
        int sizeNeeded = DocumentProperties(this.Handle, IntPtr.Zero, printerSettings.PrinterName, IntPtr.Zero, pDevMode, 0);
        IntPtr devModeData = Marshal.AllocHGlobal(sizeNeeded);
        DocumentProperties(this.Handle, IntPtr.Zero, printerSettings.PrinterName, IntPtr.Zero, pDevMode, 14);
        GlobalUnlock(hDevMode);
        printerSettings.SetHdevmode(devModeData);
        printerSettings.DefaultPageSettings.SetHdevmode(devModeData);
        GlobalFree(hDevMode);
        Marshal.FreeHGlobal(devModeData);
    }
```

## Sample Code:
```cs
private void OpenPrinterPropertiesDialog(PrinterSettings printerSettings)
    {
        IntPtr hDevMode = printerSettings.GetHdevmode(printerSettings.DefaultPageSettings);
        IntPtr pDevMode = GlobalLock(hDevMode);
        int sizeNeeded = DocumentProperties(this.Handle, IntPtr.Zero, printerSettings.PrinterName, IntPtr.Zero, pDevMode, 0);
        IntPtr devModeData = Marshal.AllocHGlobal(sizeNeeded);
        DocumentProperties(this.Handle, IntPtr.Zero, printerSettings.PrinterName, devModeData, pDevMode, 14);
        GlobalUnlock(hDevMode);
        printerSettings.SetHdevmode(devModeData);
        printerSettings.DefaultPageSettings.SetHdevmode(devModeData);
        GlobalFree(hDevMode);
        Marshal.FreeHGlobal(devModeData);
    }
```

## Sample Code:
```cs
/* mode selections for the device mode function */
    public const uint DM_UPDATE = 1;
    public const uint DM_COPY = 2;
    public const uint DM_PROMPT = 4;
    public const uint DM_MODIFY = 8;

    public const uint DM_IN_BUFFER = DM_MODIFY;
    public const uint DM_IN_PROMPT = DM_PROMPT;
    public const uint DM_OUT_BUFFER = DM_COPY;
    public const uint DM_OUT_DEFAULT = DM_UPDATE;
```
