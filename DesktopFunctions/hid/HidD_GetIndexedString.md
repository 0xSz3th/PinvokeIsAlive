
## C# Signature:
```cs
[DllImport("hid.dll", CharSet = CharSet.Auto, SetLastError = true)]
private static extern bool HidD_GetIndexedString(SafeFileHandle HidDeviceObject, uint StringIndex, StringBuilder Buffer, uint BufferLength);
```

## VB Signature:
```cs
Declare Function HidD_GetIndexedString Lib "hid.dll" (TODO) As TODO
```
