
## C# Signature:
```cs
[DllImport("Irprops.cpl", SetLastError = true)]
static extern bool BluetoothFindNextDevice(IntPtr hFind, ref BLUETOOTH_DEVICE_INFO pbtdi);
```

## VB Signature:
```cs
<DllImport("irprops.cpl", setlasterror:=True)> _
    Private Shared Function BluetoothFindNextDevice( _
    ByVal hFind As IntPtr, _
    ByRef pbtdi As BluetoothDeviceInfo) As Integer
    End Function
```
