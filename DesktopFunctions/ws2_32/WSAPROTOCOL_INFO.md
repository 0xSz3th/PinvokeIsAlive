
## C# Signature:
```cs
public int dwServiceFlags1;
    public int dwServiceFlags2;
    public int dwServiceFlags3;
    public int dwServiceFlags4;
    public int dwProviderFlags;
    public GUID ProviderId;
    public int dwCatalogEntryId;
    public WSAPROTOCOLCHAIN ProtocolChain;
    public int iVersion;
    public int iAddressFamily;
    public int iMaxSockAddr;
    public int iMinSockAddr;
    public int iSocketType;
    public int iProtocol;
    public int iProtocolMaxOffset;
    public int iNetworkByteOrder;
    public int iSecurityScheme;
    public int dwMessageSize;
    public int dwProviderReserved;
    [MarshalAs(UnmanagedType.ByValArray, SizeConst = 255 /* WSAPROTOCOL_LEN */ + 1)]
    public char[] szProtocol;
```

## C# Signature:
```cs
public int ChainLen;
    [MarshalAs(UnmanagedType.ByValArray, SizeConst = 7 /* MAX_PROTOCOL_CHAIN */)]
    public int[] ChainEntries;
```

## VB Signature:
```cs
Declare Function WSAPROTOCOL_INFO Lib "ws2_32.dll" (TODO) As TODO
```
