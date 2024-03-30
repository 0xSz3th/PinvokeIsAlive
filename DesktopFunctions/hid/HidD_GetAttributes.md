
## C# Signature:
```cs
[DllImport("hid.dll", CharSet = CharSet.Auto, SetLastError = true)]
    static extern bool HidD_GetAttributes(
        SafeFileHandle HidDeviceObject,
        ref HIDD_ATTRIBUTES Attributes);
```

## HIDD_ATTRIBUTES  Structure in C#:
```cs
[ StructLayout( LayoutKind.Sequential ) ]
public struct HIDD_ATTRIBUTES
{ 
    public Int32 Size; 
    public Int16 VendorID; 
    public Int16 ProductID
    public Int16 VersionNumber; 
}
```

## HIDD_ATTRIBUTES Structure in VB:
```cs
<StructLayout(LayoutKind.Sequential)> _
Public Structure HIDD_ATTRIBUTES
    Public Size As Int32
    Public VendorID As Int16
    Public ProductID As Int16
    Public VersionNumber As Int16
End Structure
```

## Parameters
```cs
Specifies an open handle to a top-level collection.
```

## Parameters
```cs
Pointer to a caller-allocated HIDD_ATTRIBUTES structure that returns the attributes of the collection specified by DeviceObject.
```
