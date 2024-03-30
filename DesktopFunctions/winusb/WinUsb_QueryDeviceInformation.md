
## C# Signature:
```cs
[DllImport("winusb.dll", SetLastError=true)]
static extern Boolean WinUsb_QueryDeviceInformation(
     SafeFileHandle InterfaceHandle,
     UInt32 InformationType,
     ref UInt32 BufferLength,
     byte[] Buffer);
```

## VB Signature:
```cs
Declare Function WinUsb_QueryDeviceInformation Lib "winusb.dll" (TODO) As TODO
```

## User-Defined Types:
```cs
const ULONG DEVICE_SPEED = 1;
```

## Sample Code:
```cs
UInt32 bufferLength = 100;
byte[] buffer = new byte[bufferLength];
var success = WinUsb_QueryDeviceInformation(_winUsbHandle, DEVICE_SPEED, ref bufferLength, buffer);
```
