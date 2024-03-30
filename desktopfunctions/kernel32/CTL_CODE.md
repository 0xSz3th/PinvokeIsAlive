
## C# Signature:
```cs
private static UInt32 CTL_CODE(uint DeviceType, uint Function, IOCTL_METHOD Method, IOCTL_ACCESS Access)
{
    return ((DeviceType << 16) | (((uint)Access) << 14) | (Function << 2) | ((uint)Method));
}
```

## VB Signature:
```cs
TODO: please add
```

## User-Defined Types:
```cs
private enum IOCTL_METHOD : uint
{
    METHOD_BUFFERED = 0,
    METHOD_IN_DIRECT = 1,
    METHOD_OUT_DIRECT = 2,
    METHOD_NEITHER = 3
}

private enum IOCTL_ACCESS : uint
{
    FILE_ANY_ACCESS = 0,
    FILE_READ_ACCESS = 1,
    FILE_WRITE_ACCESS = 2
}
```

## Sample Code:
```cs
UInt32 IOCTL_CUSTOM_00 = CTL_CODE(FILE_DEVICE_UNKNOWN, 0x800, IOCTL_METHOD.METHOD_BUFFERED, IOCTL_ACCESS.FILE_ANY_ACCESS);
```
