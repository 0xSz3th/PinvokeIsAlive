
## C# Signature:
```cs
[DllImport("setupapi.dll", SetLastError=true)]
static extern bool SetupDiEnumDeviceInfo(IntPtr DeviceInfoSet, uint MemberIndex, ref SP_DEVINFO_DATA DeviceInfoData);
```

## VB Signature:
```cs
<DllImport("setupapi.dll", _
    EntryPoint:="SetupDiEnumDeviceInfo", _
    SetLastError:=True, _
    CharSet:=CharSet.Unicode, _
    ExactSpelling:=True, _
    PreserveSig:=True, _
    CallingConvention:=CallingConvention.Winapi)> _
    Private Shared Function SetupDiEnumDeviceInfo( _
    ByVal DeviceInfoSet As Integer, _
    ByVal MemberIndex As Integer, _
    ByRef DeviceInfoData As SP_DEVINFO_DATA) As Boolean
    End Function
```
