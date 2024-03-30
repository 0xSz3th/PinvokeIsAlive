
## C# Signature:
```cs
[DllImport("setupapi.dll", SetLastError = true, CharSet = CharSet.Auto)]
static extern bool SetupDiGetDeviceInstanceId(
   IntPtr DeviceInfoSet,
   ref SP_DEVINFO_DATA DeviceInfoData,
   StringBuilder DeviceInstanceId,
   int DeviceInstanceIdSize,
   out int RequiredSize
);
```

## VB Signature:
```cs
Declare Function SetupDiGetDeviceInstanceId Lib "setupapi.dll" (TODO) As TODO
```

## Notes:
```cs
WINSETUPAPI BOOL WINAPI  SetupDiGetDeviceInstanceId(
   IN HDEVINFO  DeviceInfoSet,
   IN PSP_DEVINFO_DATA  DeviceInfoData,
   OUT PTSTR  DeviceInstanceId,
   IN DWORD  DeviceInstanceIdSize,
   OUT PDWORD  RequiredSize  OPTIONAL
);
```

## Sample Code:
```cs
static string GetInstanceIDByKeyName(string DriverKeyName)
    {
        string ans = "";
        string DevEnum = REGSTR_KEY_USB;

        // Use the "enumerator form" of the SetupDiGetClassDevs API 
        // to generate a list of all USB devices
        IntPtr h = SetupDiGetClassDevs(0, DevEnum, IntPtr.Zero, DIGCF_PRESENT | DIGCF_ALLCLASSES);
        if (h.ToInt32() != INVALID_HANDLE_VALUE)
        {
        IntPtr ptrBuf = Marshal.AllocHGlobal(BUFFER_SIZE);
        string KeyName;

        bool Success = true;
        int i = 0;
        while (Success)
        {
            // create a Device Interface Data structure
            SP_DEVINFO_DATA da = new SP_DEVINFO_DATA();
            da.cbSize = Marshal.SizeOf(da);

            // start the enumeration 
            Success = SetupDiEnumDeviceInfo(h, i, ref da);
            if (Success)
            {
            int RequiredSize = 0;
            int RegType = REG_SZ;

            KeyName = "";
            if (SetupDiGetDeviceRegistryProperty(h, ref da, SPDRP_DRIVER, ref RegType, ptrBuf, BUFFER_SIZE, ref RequiredSize))
            {
                KeyName = Marshal.PtrToStringAuto(ptrBuf);
            }

            // is it a match?
            if (KeyName == DriverKeyName)
            {
                int nBytes = BUFFER_SIZE;
                StringBuilder sb = new StringBuilder(nBytes);
                SetupDiGetDeviceInstanceId(h, ref da, sb, nBytes, out RequiredSize);
                ans = sb.ToString();
                break;
            }
            }
            i++;
        }
        Marshal.FreeHGlobal(ptrBuf);
        SetupDiDestroyDeviceInfoList(h);
        }
        return ans;
    }
```
