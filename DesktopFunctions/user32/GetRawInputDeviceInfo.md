
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError=true)] 
static extern uint GetRawInputDeviceInfo(IntPtr hDevice, uint uiCommand, IntPtr pData, ref uint pcbSize);
```

## C# Signature:
```cs
[DllImport("user32.dll", SetLastError = true, EntryPoint = "GetRawInputDeviceInfoA")] 
public static extern uint GetRawInputDeviceInfo(IntPtr hDevice, uint uiCommand, ref RID_DEVICE_INFO pData, ref uint pcbSize);
```

## C# Signature:
```cs
[DllImport("user32.dll", SetLastError = true, EntryPoint = "GetRawInputDeviceInfoA", CharSet = CharSet.Ansi)] 
public static extern uint GetRawInputDeviceInfo(IntPtr hDevice, uint uiCommand, StringBuilder pData, ref uint pcbSize);
```

## C# User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
    internal struct RID_DEVICE_INFO_HID
    {
        [MarshalAs(UnmanagedType.U4)]
        public int dwVendorId;
        [MarshalAs(UnmanagedType.U4)]
        public int dwProductId;
        [MarshalAs(UnmanagedType.U4)]
        public int dwVersionNumber;
        [MarshalAs(UnmanagedType.U2)]
        public ushort usUsagePage;
        [MarshalAs(UnmanagedType.U2)]
        public ushort usUsage;
    }

    [StructLayout(LayoutKind.Sequential)]
    internal struct RID_DEVICE_INFO_KEYBOARD
    {
        [MarshalAs(UnmanagedType.U4)]
        public int dwType;
        [MarshalAs(UnmanagedType.U4)]
        public int dwSubType;
        [MarshalAs(UnmanagedType.U4)]
        public int dwKeyboardMode;
        [MarshalAs(UnmanagedType.U4)]
        public int dwNumberOfFunctionKeys;
        [MarshalAs(UnmanagedType.U4)]
        public int dwNumberOfIndicators;
        [MarshalAs(UnmanagedType.U4)]
        public int dwNumberOfKeysTotal;
    }

    [StructLayout(LayoutKind.Sequential)]
    internal struct RID_DEVICE_INFO_MOUSE
    {
        [MarshalAs(UnmanagedType.U4)]
        public int dwId;
        [MarshalAs(UnmanagedType.U4)]
        public int dwNumberOfButtons;
        [MarshalAs(UnmanagedType.U4)]
        public int dwSampleRate;
        [MarshalAs(UnmanagedType.U4)]
        public int fHasHorizontalWheel;
    }
```

## C# User-Defined Types:
```cs
[StructLayout(LayoutKind.Explicit)]
    internal struct RID_DEVICE_INFO
    {
        [FieldOffset(0)]
        public int cbSize;
        [FieldOffset(4)]
        public int dwType;
        [FieldOffset(8)]
        public RID_DEVICE_INFO_MOUSE mouse;
        [FieldOffset(8)]
        public RID_DEVICE_INFO_KEYBOARD keyboard;
        [FieldOffset(8)]
        public RID_DEVICE_INFO_HID hid;
    }
    internal enum DeviceInfoTypes {
        RIDI_PREPARSEDDATA = 0x20000005,
        RIDI_DEVICENAME = 0x20000007,
        RIDI_DEVICEINFO = 0x2000000B
    }
```

## VB Signature:
```cs
Declare Function GetRawInputDeviceInfo Lib "user32.dll" Alias "GetRawInputDeviceInfoW" (ByVal hDevice As IntPtr, ByVal uiCommand As DeviceInfoTypes, ByVal pData As IntPtr, ByRef pcbSize As UInteger) As Integer
```

## VB User-Defined Types:
```cs
Public Enum DeviceInfoTypes As UInteger
     RIDI_PREPARSEDDATA = &H20000005
     RIDI_DEVICENAME = &H20000007
     RIDI_DEVICEINFO = &H2000000B
End Enum
```

## Sample Code C#:
```cs
var deviceHandle = ti.hSource; // a handle obtained from WM_TOUCH message.
        if (devBufer == null) devBufer = new StringBuilder(4096 * 2);
        devBufer.Clear();

        uint returnedDataSize = (uint)devBufer.Capacity;
        var firstCall = GetRawInputDeviceInfo(deviceHandle, RIDI_DEVICENAME, devBufer, ref returnedDataSize);
        var firstError = Marshal.GetLastWin32Error();
        var firtsDataSize = returnedDataSize;
        var devName = devBufer.ToString();
        if (string.IsNullOrEmpty(devName)) devName = "No name retrieved";

        var devInfo = new RID_DEVICE_INFO();
        var structureSize = Convert.ToUInt32(Marshal.SizeOf<RID_DEVICE_INFO>());
        devInfo.cbSize = structureSize;
        returnedDataSize = structureSize;
        var secondCall = GetRawInputDeviceInfo(deviceHandle, RIDI_DEVICEINFO, ref devInfo, ref returnedDataSize);
        var secondError = Marshal.GetLastWin32Error();
        string hidData = "ERROR: hid data retrieval failed";
        if (devInfo.dwType == 2)
        {
            hidData = devInfo.hid.ToString();
        }

        Debug.LogWarning($"New touch device detected with name '{devName}' and handle '{ti.hSource}'. " +
            $"\nWinapi calls returned '{(int)firstCall}' per name and '{(int)secondCall}' per data " +
            $"\nError codes were '{firstError}' per name and '{secondError}' per data" +
            $"\nData sizes were '{firtsDataSize}' per name and '{returnedDataSize}' per data" +
            $"\nHid data structure size: '{structureSize}'; Structure type is '{devInfo.dwType}'" +
            $"\nHid data: {hidData}");
```

## Sample Code VB:
```cs
' Enumerating devices with a known VID
    ' First half heavily borrowed from C# example on GetRawInputDeviceList()
    Sub GetAllRawDeviceVID()

         Dim deviceCount As UInt32 = 0
         Dim dwSize As Integer = CInt(Marshal.SizeOf(GetType(RAWINPUTDEVICELIST)))
         Dim retValue As UInt32 = GetRawInputDeviceList(IntPtr.Zero, deviceCount, dwSize)
         If retValue <> 0 Then Exit Sub       ' handle this

         Dim devPtr As IntPtr = Marshal.AllocHGlobal(CType(dwSize * deviceCount, Integer))
         retValue = GetRawInputDeviceList(devPtr, deviceCount, dwSize)

         Dim deviceList As RAWINPUTDEVICELIST
         Dim rawDevs As New Dictionary(Of IntPtr, RawInputDeviceType)

         For i As Integer = 0 To (deviceCount - 1)
         deviceList = CType(Marshal.PtrToStructure(New IntPtr((devPtr.ToInt32() + (dwSize * i))), GetType(RAWINPUTDEVICELIST)), RAWINPUTDEVICELIST)
         If deviceList.dwType = RawInputDeviceType.KEYBOARD Then
             rawDevs.Add(deviceList.hDevice, deviceList.dwType)
         End If

         Next

         Dim pcbSize As UInt32 = 0
         Dim deviceName As String = String.Empty
         Dim lstHDevices As New List(Of String)

         For Each itm As KeyValuePair(Of IntPtr, RawInputDeviceType) In rawDevs
         GetRawInputDeviceInfo(itm.Key, DeviceInfoTypes.RIDI_DEVICENAME, IntPtr.Zero, pcbSize)
         Dim pData As IntPtr = Marshal.AllocHGlobal(CType(pcbSize, Integer))

         GetRawInputDeviceInfo(itm.Key, DeviceInfoTypes.RIDI_DEVICENAME, pData, pcbSize)
         deviceName = Marshal.PtrToStringAuto(pData)

         If deviceName.Contains("VID_05FE") Then lstHDevices.Add(deviceName)

         Next

         ' do something

     End Sub
```
