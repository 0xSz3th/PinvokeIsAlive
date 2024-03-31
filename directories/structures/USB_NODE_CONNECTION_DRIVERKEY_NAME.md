
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
struct USB_NODE_CONNECTION_DRIVERKEY_NAME
{
   public int ConnectionIndex;
   public int ActualLength;
   [MarshalAs(UnmanagedType.ByValTStr, SizeConst = BUFFER_SIZE)]
   public string DriverKeyName;
}
```

## VB Definition:
```cs
Structure USB_NODE_CONNECTION_DRIVERKEY_NAME 
   Public TODO
End Structure
```

## Notes:
```cs
typedef struct _USB_NODE_CONNECTION_DRIVERKEY_NAME {
   ULONG  ConnectionIndex;
   ULONG  ActualLength;
   WCHAR  DriverKeyName[1];
} USB_NODE_CONNECTION_DRIVERKEY_NAME, *PUSB_NODE_CONNECTION_DRIVERKEY_NAME;
```

## Example:
```cs
// Open a handle to the Hub device
IntPtr h = CreateFile(PortHubDevicePath, GENERIC_WRITE, FILE_SHARE_WRITE, IntPtr.Zero, OPEN_EXISTING, 0, IntPtr.Zero);
if (h.ToInt32() != INVALID_HANDLE_VALUE)
{
   int nBytesReturned;

   // Get the Driver Key Name
   USB_NODE_CONNECTION_DRIVERKEY_NAME DriverKey = new USB_NODE_CONNECTION_DRIVERKEY_NAME();
   DriverKey.ConnectionIndex = PortPortNumber;
   int nBytes = Marshal.SizeOf(DriverKey);
   IntPtr ptrDriverKey = Marshal.AllocHGlobal(nBytes);
   Marshal.StructureToPtr(DriverKey, ptrDriverKey, true);

   // Use an IOCTL call to request the Driver Key Name
   if (DeviceIoControl(h, IOCTL_USB_GET_NODE_CONNECTION_DRIVERKEY_NAME, ptrDriverKey, nBytes, ptrDriverKey, nBytes, out nBytesReturned, IntPtr.Zero))
   {
     DriverKey = (USB_NODE_CONNECTION_DRIVERKEY_NAME)Marshal.PtrToStructure(ptrDriverKey, typeof(USB_NODE_CONNECTION_DRIVERKEY_NAME));
     string DeviceDriverKey = DriverKey.DriverKeyName;

   }
   Marshal.FreeHGlobal(ptrDriverKey);
   CloseHandle(h);
}
Used with DeviceIoControl and [USB_NODE_CONNECTION_DRIVERKEY_NAME] to get the "Driver Key Name" from a device on a USB Hub5/15/2017 4:52:43 AM - -94.229.131.27
```
