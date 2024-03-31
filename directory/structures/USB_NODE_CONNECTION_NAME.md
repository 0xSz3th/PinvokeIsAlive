
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
struct USB_NODE_CONNECTION_NAME
{
   public int ConnectionIndex;
   public int ActualLength;
   [MarshalAs(UnmanagedType.ByValTStr, SizeConst = BUFFER_SIZE)]
   public string NodeName;
}
```

## VB Definition:
```cs
Structure USB_NODE_CONNECTION_NAME 
   Public TODO
End Structure
```

## Notes:
```cs
typedef struct _USB_NODE_CONNECTION_NAME {
   ULONG  ConnectionIndex;
   ULONG  ActualLength;
   WCHAR  NodeName[1];
} USB_NODE_CONNECTION_NAME, *PUSB_NODE_CONNECTION_NAME;
```

## Example:
```cs
// Open a handle to the Host Controller
IntPtr h = CreateFile(PortHubDevicePath, GENERIC_WRITE, FILE_SHARE_WRITE, IntPtr.Zero, OPEN_EXISTING, 0, IntPtr.Zero);
if (h.ToInt32() != INVALID_HANDLE_VALUE)
{
   // Get the DevicePath for downstream hub
   int nBytesReturned;
   USB_NODE_CONNECTION_NAME NodeName = new USB_NODE_CONNECTION_NAME();
   NodeName.ConnectionIndex = PortPortNumber;
   int nBytes = Marshal.SizeOf(NodeName);
   IntPtr ptrNodeName = Marshal.AllocHGlobal(nBytes);
   Marshal.StructureToPtr(NodeName, ptrNodeName, true);

   // Use an IOCTL call to request the Node Name
   if (DeviceIoControl(h, IOCTL_USB_GET_NODE_CONNECTION_NAME, ptrNodeName, nBytes, ptrNodeName, nBytes, out nBytesReturned, IntPtr.Zero))
   {
     NodeName = (USB_NODE_CONNECTION_NAME)Marshal.PtrToStructure(ptrNodeName, typeof(USB_NODE_CONNECTION_NAME));
     string HubDevicePath = @"\\.\" + NodeName.NodeName;
   }
   Marshal.FreeHGlobal(ptrNodeName);
   (h);
}
Used with DeviceIoControl and [USB_NODE_CONNECTION_NAME] to get the Device Path of a device on a USB Hub5/15/2017 4:53:31 AM - -94.229.131.27
```
