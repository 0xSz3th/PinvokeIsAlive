
## C# Signature:
```cs
[DllImport("winusb.dll", SetLastError = true, CharSet = CharSet.Auto)]
static extern int WinUsb_Initialize(SafeFileHandle DeviceHandle, out IntPtr InterfaceHandle);
```
