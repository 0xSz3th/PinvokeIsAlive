
## C# Definition:
```cs
[StructLayout(LayoutKind.Explicit, Size = 24)]
    internal struct sockaddr_in6_old
    {
        [FieldOffset(0)] internal ADDRESS_FAMILIES sin6_family;

        [FieldOffset(2)] internal ushort sin6_port;

        [FieldOffset(4)] internal uint sin6_flowinfo;

        [FieldOffset(8)] internal in6_addr sin6_addr;
    }
```

## VB Definition:
```cs
Structure sockaddr_in6_old 
   Public TODO
End Structure
```
