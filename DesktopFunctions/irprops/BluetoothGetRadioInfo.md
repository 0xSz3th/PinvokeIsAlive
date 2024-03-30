
## C# Signature:
```cs
[DllImport("irprops.cpl", SetLastError=true)]
static extern TODO BluetoothGetRadioInfo(TODO);
```

## VB Signature:
```cs
<DllImport("irprops.cpl", setlasterror:=True, CharSet:=CharSet.Auto)> _
    Private Shared Function BluetoothGetRadioInfo( _
    ByVal hRadio As IntPtr, _
    ByRef pRadioInfo As BluetoothRadioInfo) As UInteger
    End Function
```

## User-Defined Types:
```cs
Private Const BLUETOOTH_MAX_NAME_SIZE = 248

    <StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Auto, pack:=1)> _
    Friend Structure BluetoothRadioInfo
        Public size As UInteger
        Public address As BluetoothAddress
        <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=BLUETOOTH_MAX_NAME_SIZE)> _
        Public name As String
        Public classofDevice As UInteger
        Public subversion As UShort
        Public manufacturer As UShort
        Public Sub Initialize()
            Me.name = New String("*"c, BLUETOOTH_MAX_NAME_SIZE)
            Me.address = New BluetoothAddress
            Me.size = Marshal.SizeOf(Me)
        End Sub
    End Structure

    ' Needs some tidying up...
    <StructLayout(LayoutKind.Sequential, pack:=1)> _
    Friend Structure BluetoothAddress
        Public byte1 As Byte
        Public byte2 As Byte
        Public byte3 As Byte
        Public byte4 As Byte
        Public byte5 As Byte    
        Public byte6 As Byte    
        Public byte7 As Byte    
        Public byte8 As Byte    
        Public byte9 As Byte    
        Public byte10 As Byte       
        Public byte11 As Byte
        Public byte12 As Byte
        Public Overrides Function ToString() As String
            ' The useful bytes...
            Return String.Format("{0}:{1}:{2}:{3}:{4}:{5}", _ 
            byte10.ToString("x"), byte9.ToString("x"), byte8.ToString("x"), _
            byte7.ToString("x"), byte6.ToString("x"), byte5.ToString("x"))
        End Function
    End Structure
```
