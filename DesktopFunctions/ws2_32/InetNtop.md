
## C# Signature:
```cs
[DllImport("Ws2_32.dll", CharSet = CharSet.Unicode, EntryPoint = "InetNtopW")]
    public static extern uint InetNtop(ADDRESS_FAMILIES Family, ref in_addr pAddr, StringBuilder pStringBuf, int StringBufSize);

    [DllImport("Ws2_32.dll", CharSet = CharSet.Unicode, EntryPoint = "InetNtopW")]
    public static extern uint InetNtop(ADDRESS_FAMILIES Family, ref in6_addr pAddr, StringBuilder pStringBuf, int StringBufSize);
```

## VB Signature:
```cs
Declare Function InetNtop Lib "ws2_32.dll" (TODO) As TODO
```
