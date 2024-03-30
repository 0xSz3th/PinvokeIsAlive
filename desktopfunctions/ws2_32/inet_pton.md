
## C# Signature:
```cs
[DllImport("Ws2_32.dll", CharSet = CharSet.Unicode, EntryPoint = "InetPtonW")]
    public static extern uint inet_pton(ADDRESS_FAMILIES Family, string pszAddrString, ref in_addr pAddrBuf);

    [DllImport("Ws2_32.dll", CharSet = CharSet.Unicode, EntryPoint = "InetPtonW")]
    public static extern uint inet_pton(ADDRESS_FAMILIES Family, string pszAddrString, ref in6_addr pAddrBuf);
```

## VB Signature:
```cs
Declare Function inet_pton Lib "ws2_32.dll" (TODO) As TODO
```
