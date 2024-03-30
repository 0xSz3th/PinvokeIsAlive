
## C# Signature:
```cs
[DllImport("Ws2_32.dll", CharSet = CharSet.Unicode, EntryPoint = "WSAAddressToStringW")]
    public static extern uint WSAAddressToString(ref sockaddr_in lpsaAddress, int dwAddressLength, IntPtr lpProtocolInfo,
        StringBuilder lpszAddressString, ref int lpdwAddressStringLength);

    [DllImport("Ws2_32.dll", CharSet = CharSet.Unicode, EntryPoint = "WSAAddressToStringW")]
    public static extern uint WSAAddressToString(ref  sockaddr_in6 lpsaAddress, int dwAddressLength, IntPtr lpProtocolInfo,
        StringBuilder lpszAddressString, ref int lpdwAddressStringLength);
```

## VB Signature:
```cs
Declare Function WSAAddressToString Lib "ws2_32.dll" (TODO) As TODO
```
