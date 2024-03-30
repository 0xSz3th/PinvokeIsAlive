
## C# Signature:
```cs
[DllImport("setupapi.dll")]
static extern int CM_Get_Parent(
   out UInt32 pdnDevInst,
   UInt32 dnDevInst,
   int ulFlags
);
```

## VB Signature:
```cs
Declare Function CM_Get_Parent Lib "setupapi.dll" (TODO) As TODO
```

## Sample Code:
```cs
Guid DiskGUID = new Guid(GUID_DEVINTERFACE_DISK);

// We start at the "root" of the device tree and look for all
// devices that match the interface GUID of a disk
IntPtr h = SetupDiGetClassDevs(ref DiskGUID, 0, IntPtr.Zero, DIGCF_PRESENT | DIGCF_DEVICEINTERFACE);
if (h.ToInt32() != INVALID_HANDLE_VALUE)
{
   bool Success = true;
   int i = 0;
   while (Success)
   {
     // create a Device Interface Data structure
     SP_DEVICE_INTERFACE_DATA dia = new SP_DEVICE_INTERFACE_DATA();
     dia.cbSize = Marshal.SizeOf(dia);

     // start the enumeration 
     Success = SetupDiEnumDeviceInterfaces(h, IntPtr.Zero, ref DiskGUID, i, ref dia);
     if (Success)
     {
    // build a DevInfo Data structure
    SP_DEVINFO_DATA da = new SP_DEVINFO_DATA();
    da.cbSize = Marshal.SizeOf(da);

    // build a Device Interface Detail Data structure
    SP_DEVICE_INTERFACE_DETAIL_DATA didd = new SP_DEVICE_INTERFACE_DETAIL_DATA();
    didd.cbSize = 4 + Marshal.SystemDefaultCharSize; // trust me :)

    // now we can get some more detailed information
    int nRequiredSize = 0;
    int nBytes = BUFFER_SIZE;
    if (SetupDiGetDeviceInterfaceDetail(h, ref dia, ref didd, nBytes, ref nRequiredSize, ref da))
    {
      // current InstanceID is at the "USBSTOR" level, so we
      // need up "move up" one level to get to the "USB" level
      UInt32 ptrPrevious;
      CM_Get_Parent(out ptrPrevious, da.DevInst, 0);

      // Now we get the InstanceID of the USB level device
      IntPtr ptrInstanceBuf = Marshal.AllocHGlobal(nBytes);
      CM_Get_Device_ID(ptrPrevious, ptrInstanceBuf, nBytes, 0);
      string InstanceID = Marshal.PtrToStringAuto(ptrInstanceBuf);

      Marshal.FreeHGlobal(ptrInstanceBuf);
    }
      }
    }
    i++;
  }
  SetupDiDestroyDeviceInfoList(h);
```
