
## C# Signature:
```cs
[DllImport("hid.dll", CharSet=CharSet.Auto, SetLastError=true)]
static extern Boolean HidD_GetManufacturerString(
            SafeFileHandle HidDeviceObject,
            StringBuilder Buffer,
            Int32 BufferLength);
```

## VB Signature:
```cs
<DllImport("hid.dll", CharSet:=CharSet.Auto, SetLastError:=True)> _
    Friend Shared Function HidD_GetManufacturerString( _
        ByVal HidDeviceObject As SafeFileHandle, _
         ByVal Buffer As System.Text.StringBuilder, _
         ByVal BufferLength As Int32) As Boolean
    End Function
```

## Sample Code:
```cs
StringBuilder manufacturerString = new StringBuilder(128);
bool returnStatus = HidD_GetManufacturerString(hidHandle, manufacturerString, manufacturerString.Capacity);
if (returnStatus)
{
     Console.WriteLine("Manufacturer name is {0}", manufacturerString.ToString());
}
```
