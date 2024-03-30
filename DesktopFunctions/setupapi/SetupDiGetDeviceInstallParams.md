
## C# Signature:
```cs
[DllImport("setupapi.dll", SetLastError=true)]
static extern TODO SetupDiGetDeviceInstallParams(TODO);
```

## VB Signature:
```cs
<DllImport("setupapi.dll")> _
Public Shared Function SetupDiGetDeviceInstallParams(ByVal hDevinfo As Integer, _  'Alternate ByVal hDevInfo as IntPtr
                              ByRef DeviceInfoData As SP_DEVINFO_DATA, _
                              ByRef DeviceInstallParams As SP_DEVINSTALL_PARAMS _
                              ) As Boolean
End Function
```

## User-Defined Types:
```cs
<StructLayout(LayoutKind.Sequential)> _
    Public Structure SP_DEVINFO_DATA
        Public cbSize As Integer
        Public ClassGuid As Guid
        Public DevInst As Integer
        Public Reserved As IntPtr
    End Structure

    <StructLayout(LayoutKind.Sequential, pack:=1)> _
    Public Structure SP_DEVINSTALL_PARAMS
        Public cbSize As Integer
        Public Flags As Integer
        Public FlagsEx As Integer
        Public hwndParent As IntPtr
        Public InstallMsgHandler As IntPtr
        Public InstallMsgHandlerContext As IntPtr
        Public FileQueue As IntPtr
        Public ClassInstallReserved As IntPtr
        Public Reserved As Integer
        <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=MAX_PATH)> _
        Public DriverPath As String
    End Structure
```

## Sample Code:
```cs
' see if device needs reboot
Dim devParams As SP_DEVINSTALL_PARAMS
devParams.cbSize = Marshal.SizeOf(devParams)
If Win32.SetupDiGetDeviceInstallParams(hDevInfo, DeviceInfoData, devParams) Then
  If (devParams.Flags And Win32.DI_NEEDRESTART) = Win32.DI_NEEDRESTART OrElse (devParams.Flags And Win32.DI_NEEDREBOOT) = Win32.DI_NEEDREBOOT Then
   Return True
  End If
Else
   Return False
End If
```
