
## C# Signature:
```cs
[DllImport("irprops.dll", SetLastError=true)]
static extern bool BluetoothIsConnectable(IntPtr hRadio);
```

## VB Signature:
```cs
<DllImport("irprops.cpl", setlasterror:=True)> _
    Private Shared Function BluetoothIsConnectable(ByVal hRadio As IntPtr) As Integer
    End Function
```
