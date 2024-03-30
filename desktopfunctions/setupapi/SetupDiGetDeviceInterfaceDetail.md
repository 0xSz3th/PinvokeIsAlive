
## C# Signature:
```cs
[DllImport(@"setupapi.dll", CharSet = CharSet.Auto, SetLastError = true)]
public static extern Boolean SetupDiGetDeviceInterfaceDetail(
   IntPtr hDevInfo,
   ref SP_DEVICE_INTERFACE_DATA deviceInterfaceData,
   ref SP_DEVICE_INTERFACE_DETAIL_DATA deviceInterfaceDetailData,
   UInt32 deviceInterfaceDetailDataSize,
   ref UInt32 requiredSize,
   ref SP_DEVINFO_DATA deviceInfoData
);
```

## VB Signature:
```cs
Public Declare Auto Function SetupDiGetDeviceInterfaceDetail2 Lib "setupapi.dll" Alias "SetupDiGetDeviceInterfaceDetailW" ( _
    ByVal hDevInfo As IntPtr, _
    ByRef deviceInterfaceData As SP_DEVICE_INTERFACE_DATA, _
    ByRef deviceInterfaceDetailData As SP_DEVICE_INTERFACE_DETAIL_DATA, _
    ByVal deviceInterfaceDetailDataSize As Int32, _
    ByRef requiredSize As Int32, _
    ByRef deviceInfoData As SP_DEVINFO_DATA) As Boolean
```

## VB.net Signature
```cs
Public Declare Auto Function SetupDiGetDeviceInterfaceDetail Lib "setupapi.dll" ( _
    ByVal DeviceInfoSet As IntPtr, _
    ByRef DeviceInterfaceData As SP_DEVICE_INTERFACE_DATA, _
    ByRef DeviceInterfaceDetailData As SP_DEVICE_INTERFACE_DETAIL_DATA, _
    ByVal DeviceInterfaceDetailDataSize As UInteger, _
    ByRef RequiredSize As UInteger, _
    ByRef DeviceInfoData As SP_DEVINFO_DATA) As Boolean '
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
       if (IntPtr.Size == 8) // for 64 bit operating systems
       didd.cbSize = 8; 
       else
       didd.cbSize = 4 + Marshal.SystemDefaultCharSize; // for 32 bit systems

       // now we can get some more detailed information
       uint nRequiredSize = 0;
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
   }
   i++;
}
SetupDiDestroyDeviceInfoList(h);
```

## Sample Code:
```cs
'goes through all devices matching the HID guid and finds one with a registry entry string matching the name of the desired HID device, in this case a Midi device

    Public Enum Reg_Types
       REG_SZ = 1
         REG_BINARY = 3
        REG_DWORD = 4
        REG_MULTI_SZ = 7
    End Enum

Function findMIDIKeyAndDescriptor() As Boolean
    Dim devEnumInterfaceResult, devDetailResult, devEnumResult, destructionResult, registryPropertyResult As Boolean
    Dim reqedBuffer As UInteger
    Dim foundIt As Boolean
    Dim startRow, searchStringPos As Integer
           Dim loopSafety As Integer
    Dim myGuid As Guid
       Dim strTemp, errorString, ControllerDeviceDesc, ControllerDriverKey As String
       Dim h, midih As IntPtr
       Dim da, da2 As SP_DEVINFO_DATA
       Dim dia As SP_DEVICE_INTERFACE_DATA
       Dim didd As SP_DEVICE_INTERFACE_DETAIL_DATA = Nothing
    Dim dwChars, errorCode As Long
        Dim bufptr As IntPtr = IntPtr.Zero
    Dim count, i, j As Integer
    Dim MidiDevName As String

    MidiDevName  = "inputwave"
          loopSafety = 2000

    Call HidD_GetHidGuid(myGuid)
    h = SetupDiGetClassDevs(myGuid, 0, IntPtr.Zero, DIGCF_PRESENT + DIGCF_DEVICEINTERFACE) '


    da.cbSize = SizeOf(da)
    dia.cbSize = SizeOf(dia)
    didd.cbSize = 6 '+' Marshal.SystemDefaultCharSize + Sizeof(intptr.zero)
    devEnumResult = True
    devEnumInterfaceResult = True
    reqedBuffer = 0




    i = -1
    foundIt = False

    Do While devEnumResult And i < loopSafety And devEnumInterfaceResult And Not foundIt
        i = i + 1
        devEnumResult = SetupDiEnumDeviceInfo(h, i, da)

        errorCode = Err.LastDllError

        devEnumInterfaceResult = SetupDiEnumDeviceInterfaces(h, IntPtr.Zero, myGuid, i, dia)

        If errorCode Then
        errorString = ErrorDescriptionDLL(errorCode)
        errorCode = 0
        End If


        If devEnumInterfaceResult And devEnumResult Then

        devDetailResult = SetupDiGetDeviceInterfaceDetail(h, dia, didd, 1000, reqedBuffer, da) 
            'reqedBuffer turns out as 170, this will be diffent on different machines/OS, 
            '1000 is used as an arbitrarly large number, i found that if this was too small then I would get an error
        errorCode = Err.LastDllError

        devDetailResult = SetupDiGetDeviceInterfaceDetail(h, dia, didd, reqedBuffer, reqedBuffer, da)

        If devDetailResult Then

            Dim RegType As UInt32 = Reg_Types.REG_SZ
            Dim RequiredSize As UInt32
            Dim KeyName As String = ""
            Dim ptrButter As IntPtr
            ptrButter = Marshal.AllocHGlobal(40)

            'get the right buffer size for the device description
            registryPropertyResult = SetupDiGetDeviceRegistryProperty(h, da, DeviceRegistryValueNames.SPDRP_DEVICEDESC, RegType, ptrButter, 0, RequiredSize)
            ptrButter = Marshal.AllocHGlobal(CInt(RequiredSize))

            registryPropertyResult = SetupDiGetDeviceRegistryProperty(h, da, DeviceRegistryValueNames.SPDRP_DEVICEDESC, RegType, ptrButter, RequiredSize, RequiredSize)
            If registryPropertyResult Then
            ControllerDeviceDesc = Marshal.PtrToStringAuto(ptrButter, RequiredSize)   
            End If

            'get the right buffer size for returning the driver key
            registryPropertyResult = SetupDiGetDeviceRegistryProperty(h, da, DeviceRegistryValueNames.SPDRP_DRIVER, RegType, ptrButter, RequiredSize, RequiredSize)
            ptrButter = Marshal.AllocHGlobal(CInt(RequiredSize))

            registryPropertyResult = SetupDiGetDeviceRegistryProperty(h, da, DeviceRegistryValueNames.SPDRP_DRIVER, RegType, ptrButter, RequiredSize, RequiredSize)
            If registryPropertyResult Then
            ControllerDriverKey = Marshal.PtrToStringAuto(ptrButter, RequiredSize)

            searchStringPos = InStr(didd.DevicePath, MidiDevName)
            If searchStringPos > 0 Then
                foundIt = True
            End If
            End If

            errorCode = Err.LastDllError
        Else
            errorCode = Err.LastDllError
        End If

        End If

        errorCode = Err.LastDllError

    Loop



    destructionResult = SetupDiDestroyDeviceInfoList(h)


    If foundIt Then
        findMIDIKeyAndDescriptor = True
    Else
        findMIDIKeyAndDescriptor = False
    End If


    End Function
```
