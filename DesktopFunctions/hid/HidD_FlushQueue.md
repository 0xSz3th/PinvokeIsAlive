
## C# Signature:
```cs
[DllImport("hid.dll", SetLastError=true)]
static extern Boolean HidD_FlushQueue(SafeFileHandle HidDeviceObject);
```

## VB Signature:
```cs
Declare Function HidD_FlushQueue Lib "hid.dll" (SafeFileHandle HidDeviceObject) As Boolean
```
