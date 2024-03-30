
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, Pack=1)]
struct USB_HUB_DESCRIPTOR
{
   public byte bDescriptorLength;
   public byte bDescriptorType;
   public byte bNumberOfPorts;
   public short wHubCharacteristics;
   public byte bPowerOnToPowerGood;
   public byte bHubControlCurrent;
   [MarshalAs(UnmanagedType.ByValArray, SizeConst = 64)]
   public byte[] bRemoveAndPowerMask;
}
```

## VB Definition:
```cs
Structure USB_HUB_DESCRIPTOR 
   Public TODO
End Structure
```

## Notes:
```cs
typedef struct _USB_HUB_DESCRIPTOR {
   UCHAR  bDescriptorLength;
   UCHAR  bDescriptorType;
   UCHAR  bNumberOfPorts;
   USHORT  wHubCharacteristics;
   UCHAR  bPowerOnToPowerGood;
   UCHAR  bHubControlCurrent;
   UCHAR  bRemoveAndPowerMask[64];
} USB_HUB_DESCRIPTOR, *PUSB_HUB_DESCRIPTOR;
```
