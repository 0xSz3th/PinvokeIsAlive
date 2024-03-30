
## C# Signature:
```cs
[DllImport("user32.dll", CharSet = CharSet.Auto)]
static extern bool EnumDisplayDevices(string lpDevice, uint iDevNum, ref DISPLAY_DEVICE lpDisplayDevice, uint dwFlags);
```

## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool EnumDisplayDevices(string lpDevice, uint iDevNum, ref DISPLAY_DEVICE lpDisplayDevice, uint dwFlags);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", EntryPoint:="EnumDisplayDevices", CharSet:=CharSet.Auto, CallingConvention:=CallingConvention.StdCall)> _
Public Shared Function EnumDisplayDevices(ByVal lpDevice As String, ByVal iDevNum As UInteger, ByRef lpDisplayDevice As DISPLAY_DEVICE, ByVal dwFlags As UInteger) As Integer
End Function
```

## Sample Code:
```cs
DISPLAY_DEVICE d=new DISPLAY_DEVICE();
    d.cb=Marshal.SizeOf(d);
    try {
        for (uint id=0; EnumDisplayDevices(null, id, ref d, 0); id++) {
            Console.WriteLine(
                String.Format("{0}, {1}, {2}, {3}, {4}, {5}",
                         id, 
                         d.DeviceName,
                         d.DeviceString,
                         d.StateFlags,
                         d.DeviceID,
                         d.DeviceKey
                         )
                          );
            d.cb=Marshal.SizeOf(d);
        }
    } catch (Exception ex) {
        Console.WriteLine(String.Format("{0}",ex.ToString()));
    }
```

## Sample VB.NET Code:
```cs
'Tested with VisualStudio 2010, Windows 7 x64

    Dim i, numberOfInterfaces as Integer
    Dim dispDev1 As New DISPLAY_DEVICE
    dispDev1.cb = Marshal.SizeOf(dispDev1)

    'First we have to enumerate the adapters.
    i = 0
    While (EnumDisplayDevices(vbNullString, i, dispDev1, &H0))
        i += 1
    End While
    numberOfInterfaces = i

    'Once we know how many adapters there are, we'll loop and retrieve some data
    For i = 0 to numberOfInterfaces - 1
        EnumDisplayDevices(vbNullString, i, dispDev1, &H0)
        TextBox1.AppendText("-=Adapter=-" & vbCrLf)
        TextBox1.AppendText("deviceName:" & dispDev1.DeviceName & vbCrLf)
        TextBox1.AppendText("deviceString:" & dispDev1.DeviceString & vbCrLf)
        TextBox1.AppendText("deviceFlags:" & dispDev1.StateFlags & vbCrLf)
        TextBox1.AppendText("-=Monitor=-" & vbCrLf)
        EnumDisplayDevices(dispDev1.DeviceName, 0, dispDev1, &H1)
        TextBox1.AppendText("deviceName:" & dispDev1.DeviceName & vbCrLf)
        TextBox1.AppendText("deviceString:" & dispDev1.DeviceString & vbCrLf)
        TextBox1.AppendText("deviceFlags:" & dispDev1.StateFlags & vbCrLf)
        TextBox1.AppendText("--" & vbCrLf)
    Next
```
