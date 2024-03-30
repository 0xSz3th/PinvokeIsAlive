
## C# Signature:
```cs
[DllImport("setupapi.dll", CharSet = CharSet.Auto)]
static extern IntPtr SetupDiGetClassDevs(
                                              ref Guid ClassGuid,
                                              [MarshalAs(UnmanagedType.LPTStr)] string Enumerator,
                                              IntPtr hwndParent,
                                              uint Flags
                                             );
```

## Alternate Signatures:
```cs
[DllImport("setupapi.dll", CharSet = CharSet.Auto)]
static extern IntPtr SetupDiGetClassDevs(           // 1st form using a ClassGUID only, with null Enumerator
   ref Guid ClassGuid,
   IntPtr Enumerator,
   IntPtr hwndParent,
   int Flags
);

[DllImport("setupapi.dll", CharSet = CharSet.Auto)]     // 2nd form uses an Enumerator only, with null ClassGUID 
static extern IntPtr SetupDiGetClassDevs(
   IntPtr ClassGuid,
   [MarshalAs(UnmanagedType.LPTStr)] string Enumerator,
   IntPtr hwndParent,
   int Flags
);
```

## Alternate Signatures:
```cs
[Flags]
        public enum DiGetClassFlags : uint {
            DIGCF_DEFAULT       = 0x00000001,  // only valid with DIGCF_DEVICEINTERFACE
            DIGCF_PRESENT       = 0x00000002,
            DIGCF_ALLCLASSES    = 0x00000004,
            DIGCF_PROFILE       = 0x00000008,
            DIGCF_DEVICEINTERFACE   = 0x00000010,
        }
```

## VB Signatures:
```cs
<DllImport("setupapi.dll", _
    EntryPoint:="SetupDiGetClassDevsW", _
    SetLastError:=True, _
    CharSet:=CharSet.Unicode, _
    ExactSpelling:=True, _
    PreserveSig:=True, _
    CallingConvention:=CallingConvention.Winapi)> _
    Private Shared Function SetupDiGetClassDevs( _
    ByRef ClassGuid As GUID, _
    ByVal Enumerator As Integer, _
    ByVal hwndParent As Integer, _
    ByVal Flags As Integer) As Integer
    End Function
```

## VB Signatures:
```cs
<DllImport("setupapi.dll", _
    EntryPoint:="SetupDiGetClassDevsW", _
    SetLastError:=True, _
    CharSet:=CharSet.Unicode, _
    ExactSpelling:=True, _
    PreserveSig:=True, _
    CallingConvention:=CallingConvention.Winapi)> _
    Private Shared Function SetupDiGetClassDevs( _
    ByRef ClassGuid As GUID, _
    ByVal samDesired As Integer, _
    ByVal Flags As Integer, _
    ByRef hwndParent As String, _
    ByVal Reserved As Integer) As Integer
    End Function
```

## VB Signatures:
```cs
Public Declare Auto Function SetupDiGetClassDevs Lib "setupapi.dll" Alias "SetupDiGetClassDevsW" ( _
    ByRef ClassGuid As Guid, _
    ByVal Enumerator As IntPtr, _
    ByVal hwndParent As IntPtr, _
    ByVal Flags As UInteger) As IntPtr
```

## User-Defined Types:
```cs
const int DIGCF_DEFAULT = 0x1;
const int DIGCF_PRESENT = 0x2;
const int DIGCF_ALLCLASSES = 0x4;
const int DIGCF_PROFILE = 0x8;
const int DIGCF_DEVICEINTERFACE = 0x10;
Guid GUID_DEVINTERFACE_DISK = new Guid(0x53f56307, 0xb6bf, 0x11d0, 0x94, 0xf2, 0x00, 0xa0, 0xc9, 0x1e, 0xfb, 0x8b);
```

## Sample Code:
```cs
Guid DiskGUID = new Guid(GUID_DEVINTERFACE_DISK);

// We start at the "root" of the device tree and look for all
// devices that match the interface GUID of a disk
IntPtr h = SetupDiGetClassDevs(ref DiskGUID, IntPtr.Zero, IntPtr.Zero, DIGCF_PRESENT | DIGCF_DEVICEINTERFACE);
if (h != (IntPtr)INVALID_HANDLE_VALUE)
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
     IntPtr ptrPrevious;
     CM_Get_Parent(out ptrPrevious, da.DevInst, 0);

     // Now we get the InstanceID of the USB level device
     IntPtr ptrInstanceBuf = Marshal.AllocHGlobal(nBytes);
     CM_Get_Device_ID(ptrPrevious, ptrInstanceBuf, nBytes, 0);
     string InstanceID = Marshal.PtrToStringAuto(ptrInstanceBuf);

     Marshal.FreeHGlobal(ptrInstanceBuf);
       }
     }
     i++;
   }
}
SetupDiDestroyDeviceInfoList(h);
```
