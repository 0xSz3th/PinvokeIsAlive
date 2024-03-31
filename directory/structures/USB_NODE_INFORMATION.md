
## C# Definition:
```cs
// We need a separate struct to hold the union due to the fact that on 64-bit USB_HUB_NODE gets marshaled
// as 8 bytes while on 32-bit it gets marshaled as 4 bytes. We cannot explicitly lay out the members of this
// struct since FieldOffset requires a constant but here FieldOffset might be 4 or 8 depending on the platform.
[StructLayout(LayoutKind.Sequential)]
struct USB_NODE_INFORMATION
{
   public USB_HUB_NODE NodeType;    /* hub, mi parent */
   public UsbNodeUnion u;
}

// Simpler version if you do not care about USB_MI_PARENT_INFORMATION
[StructLayout(LayoutKind.Sequential)]
struct USB_NODE_INFORMATION
{
   public int NodeType;
   public USB_HUB_INFORMATION HubInformation;      // Yeah, I'm assuming we'll just use the first form
}
```

## VB Definition:
```cs
Structure USB_NODE_INFORMATION 
   Public TODO
End Structure
```

## User-Defined Field Types:
```cs
enum USB_HUB_NODE : uint
{
   UsbHub,
   UsbMIParent
}

[StructLayout(LayoutKind.Sequential)]
struct USB_MI_PARENT_INFORMATION
{
   public uint NumberOfInterfaces;
};

// Separate union where we explicitly lay out the members
[StructLayout(LayoutKind.Explicit)]
struct UsbNodeUnion
{
   [FieldOffset(0)]
   public USB_HUB_INFORMATION HubInformation;
   [FieldOffset(0)]
   public USB_MI_PARENT_INFORMATION MiParentInformation;
}
```

## Notes:
```cs
typedef struct _USB_NODE_INFORMATION {
   USB_HUB_NODE  NodeType;
   union {
     USB_HUB_INFORMATION  HubInformation;
     USB_MI_PARENT_INFORMATION  MiParentInformation;
   } u;
} USB_NODE_INFORMATION, *PUSB_NODE_INFORMATION;
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
