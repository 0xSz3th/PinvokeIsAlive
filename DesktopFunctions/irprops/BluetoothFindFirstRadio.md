
## C# Signature:
```cs
[DllImport("irprops.cpl", SetLastError=true)]
static extern IntPtr BluetoothFindFirstRadio(ref Bluetooth_Find_Radio_Params pbtfrp,out IntPtr phRadio );
```

## VB Signature:
```cs
<DllImport("irprops.cpl", SetLastError:=True, CharSet:=CharSet.Auto)> _
    Private Shared Function BluetoothFindFirstRadio( _
    <[In]()> ByRef findRadioParams As BluetoothFindRadioParams, _
    <Out()> ByRef hRadio As IntPtr) As IntPtr
    End Function
```

## User-Defined Types:
```cs
Private Structure BluetoothFindRadioParams
        Public size As UInteger
        Public Sub Initialize()
                Me.size = Marshal.SizeOf(GetType(BluetoothFindRadioParams))
        End Sub    
    End Structure
```

## Sample Code:
```cs
class Bluetooth
  {
    public Bluetooth()
    {
        BLUETOOTH_FIND_RADIO_PARAM parameters = new BLUETOOTH_FIND_RADIO_PARAM();
        parameters.Initialize();

        IntPtr firstRadio;
        IntPtr nextRadio;
        nextRadio = BluetoothFindFirstRadio(ref parameters, out firstRadio);

        //work with bluetooth
        CloseHandle(firstRadio);
        CloseHandle(nextRadio);        
    }
    /// <summary>
    /// The BLUETOOTH_FIND_RADIO_PARAMS structure facilitates enumerating installed Bluetooth radios.
    /// </summary>
    [StructLayout(LayoutKind.Sequential)]
    private struct BLUETOOTH_FIND_RADIO_PARAM
    {
        internal UInt32 dwSize;
        internal void Initialize()
        {
        this.dwSize = (UInt32)Marshal.SizeOf(typeof(BLUETOOTH_FIND_RADIO_PARAM));
        }
    }

    /// <summary>
    /// Closes an open object handle.
    /// </summary>
    /// <param name="handle">[In] A valid handle to an open object.</param>
    /// <returns>If the function succeeds, the return value is nonzero. If the function fails, the return value is zero. To get extended error information, call GetLastError.</returns>
    [DllImport("Kernel32.dll", SetLastError = true)]
    static extern bool CloseHandle(IntPtr handle);

    /// <summary>
    /// Finds the first bluetooth radio present in device manager
    /// </summary>
    /// <param name="pbtfrp">Pointer to a BLUETOOTH_FIND_RADIO_PARAMS structure</param>
    /// <param name="phRadio">Pointer to where the first enumerated radio handle will be returned. When no longer needed, this handle must be closed via CloseHandle.</param>
    /// <returns>In addition to the handle indicated by phRadio, calling this function will also create a HBLUETOOTH_RADIO_FIND handle for use with the BluetoothFindNextRadio function.
    /// When this handle is no longer needed, it must be closed via the BluetoothFindRadioClose.
    /// Returns NULL upon failure. Call the GetLastError function for more information on the error. The following table describe common errors:</returns>
    [DllImport("irprops.cpl", SetLastError = true)]
    static extern IntPtr BluetoothFindFirstRadio(ref BLUETOOTH_FIND_RADIO_PARAM pbtfrp, out IntPtr phRadio);
  }
```
