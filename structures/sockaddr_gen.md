
## C# Definition:
```cs
[StructLayout(LayoutKind.Explicit, Size = 24)]
    internal struct sockaddr_gen
    {
        //[FieldOffset(0)]
        //internal sockaddr Address;

        //[FieldOffset(0)]
        //internal sockaddr_in AddressIn;

        [FieldOffset(0)] internal sockaddr_in6_old AddressIn6;
    }
```

## VB Definition:
```cs
Structure sockaddr_gen 
   Public TODO
End Structure
```
