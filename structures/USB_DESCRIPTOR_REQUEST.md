
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
struct USB_SETUP_PACKET
{
   public byte bmRequest;
   public byte bRequest;
   public short wValue;
   public short wIndex;
   public short wLength;
}
[StructLayout(LayoutKind.Sequential)]
struct USB_DESCRIPTOR_REQUEST
{
   public int ConnectionIndex;
   public USB_SETUP_PACKET SetupPacket;
   //public byte[] Data;
}
```

## VB Definition:
```cs
Structure USB_DESCRIPTOR_REQUEST 
   Public TODO
End Structure
```

## User-Defined Field Types:
```cs
const int USB_DEVICE_DESCRIPTOR_TYPE = 1;
const int USB_STRING_DESCRIPTOR_TYPE = 3;
```

## Notes:
```cs
typedef struct _USB_DESCRIPTOR_REQUEST {
   ULONG ConnectionIndex;
   struct {
     UCHAR  bmRequest;
     UCHAR  bRequest;
     USHORT  wValue;
     USHORT  wIndex;
     USHORT  wLength;
   } SetupPacket;
   UCHAR  Data[0];
} USB_DESCRIPTOR_REQUEST, *PUSB_DESCRIPTOR_REQUEST
```

## Example:
```cs
if (PortDeviceDescriptor.iManufacturer > 0) {
   int nBytesReturned;
   int nBytes = BUFFER_SIZE;

   // build a request for string descriptor
   USB_DESCRIPTOR_REQUEST Request = new USB_DESCRIPTOR_REQUEST();
   Request.ConnectionIndex = PortPortNumber;
   Request.SetupPacket.wValue = (short)((USB_STRING_DESCRIPTOR_TYPE << 8) + PortDeviceDescriptor.iManufacturer);
   Request.SetupPacket.wLength = (short)(nBytes - Marshal.SizeOf(Request));
   Request.SetupPacket.wIndex = 0x409; // Language Code

   // Geez, I wish C# had a Marshal.MemSet() method
   string NullString = new string((char)0, nBytes  / Marshal.SystemDefaultCharSize);
   IntPtr ptrRequest = Marshal.StringToHGlobalAuto(NullString);
   Marshal.StructureToPtr(Request, ptrRequest, true);

   // Use an IOCTL call to request the String Descriptor
   if (DeviceIoControl(h, IOCTL_USB_GET_DESCRIPTOR_FROM_NODE_CONNECTION, ptrRequest, nBytes, ptrRequest, nBytes, out nBytesReturned, IntPtr.Zero))
   {
     // The location of the string descriptor is immediately after
     // the Request structure.  Because this location is not "covered"
     // by the structure allocation, we're forced to zero out this
     // chunk of memory by using the StringToHGlobalAuto() hack above
     IntPtr ptrStringDesc = new IntPtr(ptrRequest.ToInt32() + Marshal.SizeOf(Request));
     USB_STRING_DESCRIPTOR StringDesc = (USB_STRING_DESCRIPTOR)Marshal.PtrToStructure(ptrStringDesc, typeof(USB_STRING_DESCRIPTOR));
     string DeviceManufacturer = StringDesc.bString;
   }
   Marshal.FreeHGlobal(ptrRequest);
}
Used with DeviceIoControl and [USB_DESCRIPTOR_REQUEST] to get either a [USB_STRING_DESCRIPTOR] or [USB_DEVICE_DESCRIPTOR] from a device on a USB Hub13/05/2007 21:03:57 - egray1@hot.rr.com-24.26.210.211Retrieve Manufacturer, Product, and SerialNumber strings from a USB device13/05/2007 05:16:39 - egray1@hot.rr.com-24.26.210.211Used by DeviceIoControl and [IOCTL_USB_GET_DESCRIPTOR_FROM_NODE_CONNECTION] to get the Device Descriptor of a device on a port on a USB Hub13/05/2009 20:05:47 - kfank-63.64.68.239
```
