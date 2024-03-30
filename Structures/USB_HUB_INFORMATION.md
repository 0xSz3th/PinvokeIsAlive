
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
struct USB_HUB_INFORMATION
{
   public USB_HUB_DESCRIPTOR HubDescriptor;
   public byte HubIsBusPowered;
}
```

## VB Definition:
```cs
Structure USB_HUB_INFORMATION 
   Public TODO
End Structure
```

## Notes:
```cs
typedef struct _USB_HUB_INFORMATION {
   USB_HUB_DESCRIPTOR HubDescriptor;
   BOOLEAN HubIsBusPowered;
} USB_HUB_INFORMATION, *PUSB_HUB_INFORMATION;
```

## Example:
```cs
IntPtr h = CreateFile(Root.HubDevicePath, GENERIC_WRITE, FILE_SHARE_WRITE, IntPtr.Zero, OPEN_EXISTING, 0, IntPtr.Zero);
if (h.ToInt32() != INVALID_HANDLE_VALUE)
{
   USB_NODE_INFORMATION NodeInfo = new USB_NODE_INFORMATION();
   NodeInfo.NodeType = (int)USB_HUB_NODE.UsbHub;
   int nBytes = Marshal.SizeOf(NodeInfo);
   IntPtr ptrNodeInfo = Marshal.AllocHGlobal(nBytes);
   Marshal.StructureToPtr(NodeInfo, ptrNodeInfo, true);

   // get the Hub Information
   if (DeviceIoControl(h2, IOCTL_USB_GET_NODE_INFORMATION, ptrNodeInfo, nBytes, ptrNodeInfo, nBytes, out nBytesReturned, IntPtr.Zero))
   {
     NodeInfo = (USB_NODE_INFORMATION)Marshal.PtrToStructure(ptrNodeInfo, typeof(USB_NODE_INFORMATION));
       // Do something here
   }
   Marshal.FreeHGlobal(ptrNodeInfo);
   CloseHandle(h);
}
Used with DeviceIoControl and [USB_NODE_INFORMATION] to get information about ports on a USB Hub5/15/2017 4:53:40 AM - -94.229.131.27
```
