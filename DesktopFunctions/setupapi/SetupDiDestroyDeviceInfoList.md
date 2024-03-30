
## C# Signature:
```cs
[DllImport("setupapi.dll", SetLastError = true)]
public static extern bool SetupDiDestroyDeviceInfoList
( 
     IntPtr DeviceInfoSet
);
```

## VB Signature:
```cs
<DllImport("setupapi.dll", _
    EntryPoint:="SetupDiDestroyDeviceInfoList", _
    SetLastError:=True, _
    ExactSpelling:=True, _
    PreserveSig:=True, _
    CallingConvention:=CallingConvention.Winapi)> _
    Private Shared Function SetupDiDestroyDeviceInfoList( _
    ByVal DeviceInfoSet As Integer) As Boolean
    End Function
```
