
## C# Signature:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct INTERFACE_INFO
    {
        public uint iiFlags;
        public sockaddr_gen iiAddress;
        public sockaddr_gen iiBroadcastAddress;
        public sockaddr_gen iiNetmask;
    }
```

## VB Signature:
```cs
Declare Function INTERFACE_INFO Lib "ws2_32.dll" (TODO) As TODO
```
