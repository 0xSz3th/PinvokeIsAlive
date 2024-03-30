
## C# Signature:
```cs
[DllImport(@"setupapi.dll", CharSet=CharSet.Auto, SetLastError = true)]
public static extern Boolean SetupDiEnumDeviceInterfaces(
   IntPtr hDevInfo,
   ref SP_DEVINFO_DATA devInfo,
   ref Guid interfaceClassGuid,
   UInt32 memberIndex,
   ref SP_DEVICE_INTERFACE_DATA deviceInterfaceData
);
```

## C# Signature (alternate):
```cs
[DllImport(@"setupapi.dll", CharSet = CharSet.Auto, SetLastError = true)]
public static extern Boolean SetupDiEnumDeviceInterfaces(
   IntPtr hDevInfo,
   IntPtr devInfo,
   ref Guid interfaceClassGuid,
   UInt32 memberIndex,
   ref SP_DEVICE_INTERFACE_DATA deviceInterfaceData
);
```

## VB Signature:
```cs
<DllImport("setupapi.dll", CharSet:=CharSet.Auto, SetLastError:=True)> _
  Public Shared Function SetupDiEnumDeviceInterfaces(ByVal hDevInfo As IntPtr, _
    ByRef devInfo As SP_DEVICE_INTERFACE_DATA, ByRef interfaceClassGuid As Guid, _
    ByVal memberIndex As UInt32, ByRef deviceInterfaceData As SP_DEVICE_INTERFACE_DATA) As Boolean
  End Function
```

## VB 9 Signature:
```cs
Public Declare Auto Function SetupDiEnumDeviceInterfaces Lib "setupapi.dll" ( _
    ByVal DeviceInfoSet As IntPtr, _
    ByVal DeviceInfoData As UInteger, _
    ByRef InterfaceClassGuid As Guid, _
    ByVal MemberIndex As UInteger, _
    ByRef DeviceInterfaceData As SP_DEVICE_INTERFACE_DATA) As Boolean
```

## Tips & Tricks:
```cs
bool result = Win32Calls.SetupDiEnumDeviceInterfaces(ipDeviceHndl, iLU, ref DeviceGUID, 0, ref devData);
```

## Sample Code:
```cs
class Win32Calls
    {
    [DllImport(@"setupapi.dll", CharSet = CharSet.Auto, SetLastError = true)]
    public static extern IntPtr SetupDiGetClassDevs(ref Guid classGuid, IntPtr enumerator, IntPtr hwndParent, UInt32 flags);
    [DllImport(@"setupapi.dll", CharSet = CharSet.Auto, SetLastError = true)]
    public static extern Boolean SetupDiEnumDeviceInterfaces(IntPtr hDevInfo, IntPtr devInfo, ref Guid interfaceClassGuid, UInt32 memberIndex, ref SP_DEVICE_INTERFACE_DATA deviceInterfaceData);

    }
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
   int i = 0;            //To author: Could you, please, check it once again? My compiler tells me, it suppose to be uint instead of int. 
                 //Thank you.
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
       // didd.cbSize = 4 + Marshal.SystemDefaultCharSize; // trust me :) // <-- incorrect 
       didd.cbSize = IntPtr.Size == 8 ? 8 : 5; // I do not trust you (pragma pack(8) for x64)

       // now we can get some more detailed information
       int nRequiredSize = 0;
       int nBytes = BUFFER_SIZE;
       if (SetupDiGetDeviceInterfaceDetail(h, ref dia, ref didd, nBytes, ref nRequiredSize, ref da))
       {
       // current InstanceID is at the "USBSTOR" level, so we
       // need up "move up" one level to get to the "USB" level
       IntPtr ptrPrevious;
       CM_Get_Parent(out ptrPrevious, da.DevInst, 0);

       // Now we get the InstanceID of the USB level device
       IntPtr ptrInstanceBuf = Marshal.AllocHGlobal(nBytes);
       CM_Get_Device_ID(ptrPrevious, ptrInstanceBuf, nBytes, 0);
       string InstanceID = Marshal.PtrToStringAuto(ptrInstanceBuf);

       Marshal.FreeHGlobal(ptrInstanceBuf);
       }
       i++;
     }
   }
}
SetupDiDestroyDeviceInfoList(h);
```
