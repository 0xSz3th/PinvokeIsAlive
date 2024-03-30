
## C# Signature:
```cs
[DllImport("msports.dll", SetLastError=true)]
static extern int SerialDisplayAdvancedSettings(IntPtr parentHwnd, IntPtr deviceInfoSet, ref SP_DEVINFO_DATA deviceInfoData);
```

## VB Signature:
```cs
Declare Function SerialDisplayAdvancedSettings Lib "msports.dll" (TODO) As TODO
```

## Sample Code:
```cs
var deviceClassGuid = Guid.Parse("{4d36e978-e325-11ce-bfc1-08002be10318}"); // Ports class GUID
const int DIGCF_PRESENT = 0x2;
IntPtr deviceInfoSetHandle = NativeMethods.SetupDiGetClassDevs(ref deviceClassGuid, null, IntPtr.Zero, DIGCF_PRESENT);

try
{
    // search frendlyName and open advanced settings
    var deviceInfoData = new SP_DEVINFO_DATA();
    deviceInfoData.CbSize = (uint)Marshal.SizeOf(deviceInfoData);

    uint index = 0;
    while (NativeMethods.SetupDiEnumDeviceInfo(deviceInfoSetHandle, index++, ref deviceInfoData))
    {
        var buffer = new byte[300];
        const uint SPDRP_FRIENDLYNAME = 0xC;
        NativeMethods.SetupDiGetDeviceRegistryProperty(deviceInfoSetHandle, ref deviceInfoData, SPDRP_FRIENDLYNAME, out var _, buffer, (uint)buffer.Length, out var _);

        var friendlyName = Encoding.Unicode.GetString(buffer).TrimEnd('\0');
        if (friendlyName == "...")
        {
            NativeMethods.SerialDisplayAdvancedSettings(IntPtr.Zero, deviceInfoSetHandle, ref deviceInfoData);
            return;
        }
    }
}
finally
{
    NativeMethods.SetupDiDestroyDeviceInfoList(deviceInfoSetHandle);
}
```
