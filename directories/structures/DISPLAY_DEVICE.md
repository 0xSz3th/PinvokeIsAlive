
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto)]
public struct DISPLAY_DEVICE 
{
      [MarshalAs(UnmanagedType.U4)]
      public int cb;
      [MarshalAs(UnmanagedType.ByValTStr, SizeConst=32)]
      public string DeviceName;
      [MarshalAs(UnmanagedType.ByValTStr, SizeConst=128)]
      public string DeviceString;
      [MarshalAs(UnmanagedType.U4)]
      public DisplayDeviceStateFlags StateFlags;
      [MarshalAs(UnmanagedType.ByValTStr, SizeConst=128)]
      public string DeviceID;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst=128)]
      public string DeviceKey;
}
```

## VB.NET Definition:
```cs
<StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Auto)> _
Public Structure DISPLAY_DEVICE
    <MarshalAs(UnmanagedType.U4)> _
    Public cb As Integer
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=32)> _
    Public DeviceName As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=128)> _
    Public DeviceString As String
    <MarshalAs(UnmanagedType.U4)> _
    Public StateFlags As DisplayDeviceStateFlags
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=128)> _
    Public DeviceID As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=128)> _
    Public DeviceKey As String
End Structure
```
