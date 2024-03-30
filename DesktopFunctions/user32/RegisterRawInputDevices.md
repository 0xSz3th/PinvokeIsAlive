
## C# Signature:
```cs
/// <summary>Function to register a raw input device.</summary>
/// <param name="pRawInputDevices">Array of raw input devices.</param>
/// <param name="uiNumDevices">Number of devices.</param>
/// <param name="cbSize">Size of the RAWINPUTDEVICE structure.</param>
/// <returns>TRUE if successful, FALSE if not.</returns>
[DllImport("user32.dll")]
public static extern bool RegisterRawInputDevices([MarshalAs(UnmanagedType.LPArray, SizeParamIndex=0)] RAWINPUTDEVICE[] pRawInputDevices, int uiNumDevices, int cbSize);
```

## VB.NET Signature:
```cs
''' <summary>Function to register a raw input device.</summary>
''' <param name="pRawInputDevices">Array of raw input devices.</param>
''' <param name="uiNumDevices">Number of devices.</param>
''' <param name="cbSize">Size of the RAWINPUTDEVICE structure.</param>
''' <returns>True if successful, False if not.</returns>
<DllImport("user32.dll")> _
Public Shared Function RegisterRawInputDevices(<MarshalAs(UnmanagedType.LPArray, SizeParamIndex := 0)> ByVal pRawInputDevices As RAWINPUTDEVICE(), ByVal uiNumDevices As Integer, ByVal cbSize As Integer) As Boolean
End Function
```

## Sample Code:
```cs
private void RegisterMouse()
    {
        RAWINPUTDEVICE device;

        device.WindowHandle = this.Handle;
        device.UsagePage = 0x01;
        device.Usage = 0x02;
        device.Flags = RawInputDeviceFlags.InputSink;

        Win32API.RegisterRawInputDevices(device);
    }

    /// <summary>
    /// Function to register a raw input device.
    /// </summary>
    /// <param name="device">Device information.</param>
    /// <returns>TRUE if successful, FALSE if not.</returns>
    public static bool RegisterRawInputDevices(RAWINPUTDEVICE device)
    {
        RAWINPUTDEVICE[] devices = new RAWINPUTDEVICE[1];        // Raw input devices.

        devices[0] = device;
        return RegisterRawInputDevices(devices, 1, Marshal.SizeOf(typeof(RAWINPUTDEVICE)));
    }
```
