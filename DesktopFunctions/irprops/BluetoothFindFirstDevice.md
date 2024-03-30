
## C# Signature:
```cs
[DllImport("irprops.cpl", SetLastError=true)]
static extern IntPtr BluetoothFindFirstDevice(ref BLUETOOTH_DEVICE_SEARCH_PARAMS searchParams, ref BLUETOOTH_DEVICE_INFO deviceInfo);
```

## VB Signature:
```cs
<DllImport("irprops.cpl", setlasterror:=True, CharSet:=CharSet.Auto)> _
    Private Shared Function BluetoothFindFirstDevice( _
    <[In]()> ByRef searchParams As BluetoothDeviceSearchParams, _
    ByRef deviceInfo As BluetoothDeviceInfo) As IntPtr
    End Function
```

## User-Defined Types:
```cs
Private Const BLUETOOTH_MAX_NAME_SIZE = 248

    <StructLayout(LayoutKind.Sequential, pack:=4)> _
    Private Structure BluetoothDeviceSearchParams
        Public size As UInteger        ' 32 (pack = 4!)
        Public returnAuthenticated As Integer
        Public returnRemembered As Integer
        Public returnUnknown As Integer
        Public returnConnected As Integer
        Public issueInquiry As Integer
        Public timeoutMultiplier As Byte
        Public hRadio As IntPtr
    End Structure

    <StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Auto, Pack:=1)> _
    Private Structure BluetoothDeviceInfo
        Public size As UInteger        ' 560
        Public address As BluetoothAddress
        Public classofDevice As UInteger
        Public connected As Boolean
        Public remembered As Boolean
        Public authenticated As Boolean
        Public lastSeen As SystemTime
        Public lastUsed As SystemTime
        <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=BLUETOOTH_MAX_NAME_SIZE)> _
        Public name As String
        Public Sub Initialize()
            Me.name = New String("*"c, BLUETOOTH_MAX_NAME_SIZE)
            Me.lastSeen = New SystemTime
            Me.lastUsed = New SystemTime
            Me.size = Marshal.SizeOf(Me)
        End Sub
    End Structure

    <StructLayout(LayoutKind.Sequential, pack:=1)> _
    Private Structure SystemTime
        Public year As UShort
        Public month As UShort
        Public dayOfWeek As UShort
        Public day As UShort
        Public hour As UShort
        Public minute As UShort
        Public second As UShort
        Public milliseconds As UShort
    End Structure

    ' ugly. It looks like a DWORD is missing from the start ?!?
    <StructLayout(LayoutKind.Sequential, pack:=1)> _
    Private Structure BluetoothAddress
        Public byte1 As Byte
        Public byte2 As Byte
        Public byte3 As Byte
        Public byte4 As Byte
        Public byte5 As Byte    ' these
        Public byte6 As Byte    ' are 
        Public byte7 As Byte    ' the
        Public byte8 As Byte    ' six
        Public byte9 As Byte    ' address
        Public byte10 As Byte    ' bytes
        Public byte11 As Byte
        Public byte12 As Byte
        Public Overrides Function ToString() As String
            Return String.Format("{0}:{1}:{2}:{3}:{4}:{5}", byte10.ToString("x"), byte9.ToString("x"), _
                   byte8.ToString("x"), byte7.ToString("x"), byte6.ToString("x"), byte5.ToString("x"))
        End Function
    End Structure
```
