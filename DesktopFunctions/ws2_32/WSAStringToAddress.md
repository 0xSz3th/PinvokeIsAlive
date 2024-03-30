
## C# Signature:
```cs
/* converts a network address in its standard text presentation form into its numeric binary form in a sockaddr structure.  */
    [ DllImport ( "Ws2_32.dll", 
              CharSet = CharSet.Unicode, 
              EntryPoint = "WSAStringToAddressW" ) ]
    public static extern uint WSAStringToAddress ( 
                      string        AddressString, 
                      ADDRESS_FAMILIES    AddressFamily, 
                      IntPtr        lpProtocolInfo, 
                      ref sockaddr_in6    pAddr, 
                      ref int        lpAddressLength);
```

## VB Signature:
```cs
Declare Function WSAStringToAddress Lib "ws2_32.dll" (TODO) As TODO
```

## Sample Code:
```cs
WSADATA data = new WSADATA();
    SockAddr sockAddr = new SockAddr();
    IntPtr pSockAddr = IntPtr.Zero;

    if (WSAStartup(0x201, ref data) == ERROR_SUCCESS)
    {
        int sockAddrSize = Marshal.SizeOf(sockAddr);

        int result = WSAStringToAddress(
        "1.2.3.4",
        System.Net.Sockets.AddressFamily.InterNetwork,
        IntPtr.Zero,
        ref sockAddr,
        ref sockAddrSize);

        WSACleanup();
    }

    if (result != ERROR_SUCCESS)
    {
         throw new Win32Exception(result);
    }

    pSockAddr = Marshal.AllocHGlobal(Marshal.SizeOf(sockAddr));
    Marshal.StructureToPtr(sockAddr, pSockAddr, true);
```
