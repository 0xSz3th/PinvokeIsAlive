
## C# Signature:
```cs
[DllImport("hid.dll", SetLastError=true)]
static extern Boolean HidD_GetFeature(SafeFileHandle HidDeviceObject, ref Byte lpReportBuffer, Int32 ReportBufferLength);
```

## VB Signature:
```cs
Declare Function HidD_GetFeature Lib "hid.dll" (ByVal HidDeviceObject As SafeFileHandle, out lpReportBuffer As Byte, ReportBufferLength As Int32) As Boolean

<DllImport("hid.dll", SetLastError:=True, CallingConvention:=CallingConvention.StdCall)> _
Public Shared Function HidD_GetFeature(hidDeviceObject As SafeFileHandle, ByVal reportBuffer As Byte(), ByVal reportBufferLength As UInt32) As Boolean
End Function
```
