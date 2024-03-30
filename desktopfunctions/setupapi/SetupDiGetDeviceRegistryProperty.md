
## C# Signature:
```cs
[DllImport("setupapi.dll", CharSet = CharSet.Auto, SetLastError = true)]
public static extern bool SetupDiGetDeviceRegistryProperty(
    IntPtr deviceInfoSet,
    ref SP_DEVINFO_DATA deviceInfoData,
    uint property,
    out UInt32 propertyRegDataType,
    byte[] propertyBuffer,
    uint propertyBufferSize,
    out UInt32 requiredSize
    );
```

## Alternate C# Signature:
```cs
[DllImport("setupapi.dll", SetLastError = true)]
public static extern bool SetupDiGetDeviceRegistryProperty(
    IntPtr deviceInfoSet,
    ref SP_DEVINFO_DATA deviceInfoData,
    uint property,
    out UInt32 propertyRegDataType,
    IntPtr propertyBuffer, // the difference between this signature and the one above.
    uint propertyBufferSize,
    out UInt32 requiredSize
    );
```

## VB Signature:
```cs
<DllImport("setupapi.dll", SetLastError:=True)> _
Public Shared Function SetupDiGetDeviceRegistryProperty( _
    ByVal DeviceInfoSet As Integer, _
    ByRef DeviceInfoData As SP_DEVINFO_DATA, _
    ByVal [Property] As Integer, _
    ByRef PropertyRegDataType As Integer, _ 
    ByVal PropertyBuffer As Byte(), _ 
    ByVal PropertyBufferSize As Integer, _
    ByRef RequiredSize As Integer) As Boolean
End Function
```

## Possible values for Property.
```cs
/// <summary>
/// Flags for SetupDiGetDeviceRegistryProperty().
/// </summary>
enum SetupDiGetDeviceRegistryPropertyEnum : uint
{
     SPDRP_DEVICEDESC          = 0x00000000, // DeviceDesc (R/W)
     SPDRP_HARDWAREID          = 0x00000001, // HardwareID (R/W)
     SPDRP_COMPATIBLEIDS           = 0x00000002, // CompatibleIDs (R/W)
     SPDRP_UNUSED0             = 0x00000003, // unused
     SPDRP_SERVICE             = 0x00000004, // Service (R/W)
     SPDRP_UNUSED1             = 0x00000005, // unused
     SPDRP_UNUSED2             = 0x00000006, // unused
     SPDRP_CLASS               = 0x00000007, // Class (R--tied to ClassGUID)
     SPDRP_CLASSGUID           = 0x00000008, // ClassGUID (R/W)
     SPDRP_DRIVER              = 0x00000009, // Driver (R/W)
     SPDRP_CONFIGFLAGS         = 0x0000000A, // ConfigFlags (R/W)
     SPDRP_MFG             = 0x0000000B, // Mfg (R/W)
     SPDRP_FRIENDLYNAME        = 0x0000000C, // FriendlyName (R/W)
     SPDRP_LOCATION_INFORMATION    = 0x0000000D, // LocationInformation (R/W)
     SPDRP_PHYSICAL_DEVICE_OBJECT_NAME = 0x0000000E, // PhysicalDeviceObjectName (R)
     SPDRP_CAPABILITIES        = 0x0000000F, // Capabilities (R)
     SPDRP_UI_NUMBER           = 0x00000010, // UiNumber (R)
     SPDRP_UPPERFILTERS        = 0x00000011, // UpperFilters (R/W)
     SPDRP_LOWERFILTERS        = 0x00000012, // LowerFilters (R/W)
     SPDRP_BUSTYPEGUID         = 0x00000013, // BusTypeGUID (R)
     SPDRP_LEGACYBUSTYPE           = 0x00000014, // LegacyBusType (R)
     SPDRP_BUSNUMBER           = 0x00000015, // BusNumber (R)
     SPDRP_ENUMERATOR_NAME         = 0x00000016, // Enumerator Name (R)
     SPDRP_SECURITY            = 0x00000017, // Security (R/W, binary form)
     SPDRP_SECURITY_SDS        = 0x00000018, // Security (W, SDS form)
     SPDRP_DEVTYPE             = 0x00000019, // Device Type (R/W)
     SPDRP_EXCLUSIVE           = 0x0000001A, // Device is exclusive-access (R/W)
     SPDRP_CHARACTERISTICS         = 0x0000001B, // Device Characteristics (R/W)
     SPDRP_ADDRESS             = 0x0000001C, // Device Address (R)
     SPDRP_UI_NUMBER_DESC_FORMAT       = 0X0000001D, // UiNumberDescFormat (R/W)
     SPDRP_DEVICE_POWER_DATA       = 0x0000001E, // Device Power Data (R)
     SPDRP_REMOVAL_POLICY          = 0x0000001F, // Removal Policy (R)
     SPDRP_REMOVAL_POLICY_HW_DEFAULT   = 0x00000020, // Hardware Removal Policy (R)
     SPDRP_REMOVAL_POLICY_OVERRIDE     = 0x00000021, // Removal Policy Override (RW)
     SPDRP_INSTALL_STATE           = 0x00000022, // Device Install State (R)
     SPDRP_LOCATION_PATHS          = 0x00000023, // Device Location Paths (R)
     SPDRP_BASE_CONTAINERID        = 0x00000024  // Base ContainerID (R)
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
          // get the Device Description and DriverKeyName
          Uint32 RequiredSize;
          Uint32 RegType;
          byte[] buffer = new byte[BUFFER_SIZE];

          if (SetupDiGetDeviceRegistryProperty(h, ref da, SPDRP_DEVICEDESC, out RegType, buffer, BUFFER_SIZE, out RequiredSize))
          {
            string ControllerDeviceDesc = Encoding.Unicode.GetString(buffer).TrimEnd('\0');
          }
          if (SetupDiGetDeviceRegistryProperty(h, ref da, SPDRP_DRIVER, out RegType, buffer, BUFFER_SIZE, out RequiredSize))
          {
            string ControllerDriverKeyName = Encoding.Unicode.GetString(buffer).TrimEnd('\0');
          }
       }
     }
   }
   i++;
}
SetupDiDestroyDeviceInfoList(h);
```

## Alternative Sample Code:
```cs
IntPtr ptrBuffer = new IntPtr();
ptrBuffer = Marshal.AllocHGlobal(BUFFER_SIZE);
UInt32 RequiredSize = 0;
UInt32 regType = REG_SZ;

if ( SetupDiGetDeviceRegistryProperty(h, ref da, SPDRP_DEVICEDESC, out regType, ptrBuffer, BUFFER_SIZE, out RequiredSize) )
{
   string ControllerDeviceDesc = Marshal.PtrToStringAuto(ptrBuffer);
}

if ( SetupDiGetDeviceRegistryProperty(h, ref da, SPDRP_DRIVER, out regType, ptrBuffer, BUFFER_SIZE, out RequiredSize) )
{
   string ControllerDriverKeyName = Marshal.PtrToStringAuto(ptrBuffer);
}
Marshal.FreeHGlobal(ptrBuffer);
```
