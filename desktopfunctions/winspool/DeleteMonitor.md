
## C# Signature:
```cs
[DllImport("winspool.drv", SetLastError = true, CharSet = CharSet.Auto)]
private static extern Int32 DeleteMonitor(String pName, String pEnvironment, String pMonitorName);
```

## VB Signature:
```cs
Declare Function DeleteMonitor Lib "winspool.dll" (TODO) As TODO
```

## Sample Code:
```cs
String sErrorTitle="Removing monitor";
String szEnvironment = null;
String szMonitor="MyMonitor";

try
{
   if (DeleteMonitor(null, szEnvironment, szMonitor) == 0)
   {
     string errorMessage = new Win32Exception(Marshal.GetLastWin32Error()).Message;
     MessageBox.Show(String.Format("Deleting the monitor failed.\n\nError: {0}", errorMessage), sErrorTitle, MessageBoxButtons.OK, MessageBoxIcon.Error);

     return;
   }
}
catch (Exception ex)
{
   MessageBox.Show(String.Format("Deleting the monitor failed.\n\nException: {0}", ex.ToString()), sErrorTitle, MessageBoxButtons.OK, MessageBoxIcon.Error);
}
```
