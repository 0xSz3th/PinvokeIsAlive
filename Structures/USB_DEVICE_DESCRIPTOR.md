
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, Pack=1)]
struct USB_DEVICE_DESCRIPTOR
{
   public byte bLength;
   public byte bDescriptorType;
   public ushort bcdUSB;
   public byte bDeviceClass;
   public byte bDeviceSubClass;
   public byte bDeviceProtocol;
   public byte bMaxPacketSize0;
   public ushort idVendor;
   public ushort idProduct;
   public ushort bcdDevice;
   public byte iManufacturer;
   public byte iProduct;
   public byte iSerialNumber;
   public byte bNumConfigurations;
}
```

## VB Definition:
```cs
Structure USB_DEVICE_DESCRIPTOR 
   Public TODO
End Structure
```

## Notes:
```cs
typedef struct _USB_DEVICE_DESCRIPTOR {
   UCHAR  bLength;
   UCHAR  bDescriptorType;
   USHORT  bcdUSB;
   UCHAR  bDeviceClass;
   UCHAR  bDeviceSubClass;
   UCHAR  bDeviceProtocol;
   UCHAR  bMaxPacketSize0;
   USHORT  idVendor;
   USHORT  idProduct;
   USHORT  bcdDevice;
   UCHAR  iManufacturer;
   UCHAR  iProduct;
   UCHAR  iSerialNumber;
   UCHAR  bNumConfigurations;
} USB_DEVICE_DESCRIPTOR, *PUSB_DEVICE_DESCRIPTOR ;
```
