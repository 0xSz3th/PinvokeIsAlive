
## C# Signature:
```cs
public enum RawInputDeviceType : uint
    {
        MOUSE = 0,
        KEYBOARD = 1,
        HID = 2
    }

    [StructLayout( LayoutKind.Sequential )]
    public struct RAWINPUTDEVICELIST
    {
        public IntPtr hDevice;
        public RawInputDeviceType Type;
    }

    [DllImport("user32.dll", SetLastError = true, CharSet = CharSet.Auto)]
    public static extern uint GetRawInputDeviceList
    (
        [In, Out] RAWINPUTDEVICELIST[] RawInputDeviceList,
        ref uint NumDevices,
        uint Size /* = (uint)Marshal.SizeOf(typeof(RawInputDeviceList)) */
    );
```

## VB.Net Signature:
```cs
< StructLayout( LayoutKind.Sequential )> _
    Public Structure RAWINPUTDEVICELIST
       Public hDevice as Int32
       Public dwType as UInt32
    End Structure

   <DllImport("user32.dll", CharSet:=CharSet.Auto, 
    EntryPOint:="GetRawInputDeviceList", SetLastError:=True)> _ 
    Public Function GetRawInputDeviceList(ByVal pRawInputDeviceList As 
    IntPtr, ByRef puiNumDevices As Int32, ByVal cbSize As Int32) As Int32 
    End Function
```

## VB Signature:
```cs
Declare Function GetRawInputDeviceList Lib "user32.dll" (ByVal pRawInputDeviceList As 
    IntPtr, ByRef puiNumDevices As Long, ByVal cbSize As Long) As Long
```

## Sample Code:
```cs
int structSize = Marshal.SizeOf(typeof(RAWINPUTDEVICELIST));    
int bufferCount = 10;
IntPtr buffer = Marshal.AllocHGlobal(bufferCount * structSize);

int deviceCount = GetRawInputDeviceList(buffer, ref bufferCount, structSize);

for (int i = 0; i < deviceCount; ++i)
{
    RAWINPUTDEVICELIST device = (RAWINPUTDEVICELIST)Marshal.PtrToStructure(
new IntPtr((buffer.ToInt32() + (structSize * i))),typeof(RAWINPUTDEVICELIST));
...
}

    // A convenient function for getting all raw input devices.
    // This method will get all devices, including virtual devices
    // For remote desktop and any other device driver that's registered
    // as such a device.
    public static RAWINPUTDEVICELIST[] GetAllRawDevices()
    {
       uint deviceCount = 0;
        uint dwSize = (uint)Marshal.SizeOf(typeof(RAWINPUTDEVICELIST));

        // First call the system routine with a null pointer
        // for the array to get the size needed for the list
        uint retValue = Win32API.GetRawInputDeviceList(null, ref deviceCount, dwSize);

        // If anything but zero is returned, the call failed, so return a null list
        if (0 != retValue)
        return null;

        // Now allocate an array of the specified number of entries
        RAWINPUTDEVICELIST[] deviceList = new RAWINPUTDEVICELIST[deviceCount];

        // Now make the call again, using the array
        retValue = Win32API.GetRawInputDeviceList(deviceList, ref deviceCount, dwSize);

        // Free up the memory we first got the information into as
        // it is no longer needed, since the structures have been 
        // copied to the deviceList array.
       //IntPtr pRawInputDeviceList = Marshal.AllocHGlobal((int)(dwSize * deviceCount));
       //Marshal.FreeHGlobal(pRawInputDeviceList);

        // Finally, return the filled in list
        return deviceList;
    }
```
