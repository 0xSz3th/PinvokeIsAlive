
## C# Signature:
```cs
[DllImport("setupapi.dll", SetLastError = true, CharSet = CharSet.Auto)]
static extern bool SetupDiSetClassInstallParams(IntPtr DeviceInfoSet, ref SP_DEVINFO_DATA DeviceInfoData, IntPtr ClassInstallParams, int ClassInstallParamsSize);
```

## VB Signature:
```cs
Declare Function SetupDiSetClassInstallParams Lib "setupapi.dll" (TODO) As TODO
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential, Pack = 1)]
public struct SP_DEVINFO_DATA
{
    public int cbSize;
    public Guid ClassGuid;
    public uint DevInst;
    public IntPtr Reserved;
}
```
