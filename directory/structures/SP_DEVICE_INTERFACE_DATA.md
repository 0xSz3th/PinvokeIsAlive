
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
  struct SP_DEVICE_INTERFACE_DATA
  {
    public  Int32    cbSize;
    public  Guid     interfaceClassGuid;
    public  Int32    flags;
    private UIntPtr  reserved;
  }
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _
Public Structure SP_DEVICE_INTERFACE_DATA
    Public cbSize         As UInteger
    Public interfaceClassGuid As Guid
    Public flags          As UInteger
    Public reserved       As IntPtr
End Structure
```
