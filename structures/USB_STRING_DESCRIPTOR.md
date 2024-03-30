
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto)]
struct USB_STRING_DESCRIPTOR
{
   public byte bLength;
   public byte bDescriptorType;
   [MarshalAs(UnmanagedType.ByValTStr, SizeConst=MAXIMUM_USB_STRING_LENGTH)]
   public string bString;
}
```

## VB Definition:
```cs
Structure USB_STRING_DESCRIPTOR 
   Public TODO
End Structure
```

## User-Defined Field Types:
```cs
const int MAXIMUM_USB_STRING_LENGTH = 255;
const int USB_STRING_DESCRIPTOR_TYPE = 3;
```

## Notes:
```cs
typedef struct _USB_STRING_DESCRIPTOR {
   UCHAR bLength;
   UCHAR bDescriptorType;
   WCHAR bString[1];
} USB_STRING_DESCRIPTOR, *PUSB_STRING_DESCRIPTOR;
```

## Notes:
```cs
string NullString = new string((char)0, BUFFER_SIZE / Marshal.SystemDefaultCharSize);
IntPtr ptrRequest = Marshal.StringToHGlobalAuto(NullString);
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
```
