
## C# Signature:
```cs
[DllImport("netapi32.dll", CharSet=CharSet.Auto)]
public static extern int DsAddressToSiteNames(string computerName, int entryCount, SOCKET_ADDRESS[] socketAddresses, ref IntPtr siteNames);
```

## VB Signature:
```cs
Declare Function DsAddressToSiteNames Lib "netapi32.dll" (TODO) As TODO
```

## C# Sample Code:
```cs
public static string GetSiteNameForAddress(string address)
{
    if (string.IsNullOrEmpty(address))
    {
         throw new ArgumentNullException("address");
    }

    WSADATA data = new WSADATA();
    SockAddr sockAddr = new SockAddr();
    IntPtr pSockAddr = IntPtr.Zero;
    IntPtr pSites = IntPtr.Zero;
    SOCKET_ADDRESS[] SocketAddresses = new SOCKET_ADDRESS[1];
    string siteName = string.Empty;

    if (WSAStartup(0x201, ref data) == ERROR_SUCCESS)
    {
        int sockAddrSize = Marshal.SizeOf(sockAddr);

        // Call into WSAStringToAddress to build SOCKET_ADDRESS structure from the address string
        int result = WSAStringToAddress(
            address,
            System.Net.Sockets.AddressFamily.InterNetwork,
            IntPtr.Zero,
            ref sockAddr,
            ref sockAddrSize);

        WSACleanup();

        // Check for failure from the WSAStringToAddress method
        if (result != ERROR_SUCCESS)
        {
           throw new Win32Exception(result);
        }

        // Allocate memory on the heap for the SockAddr structure
        pSockAddr = Marshal.AllocHGlobal(Marshal.SizeOf(sockAddr));
        Marshal.StructureToPtr(sockAddr, pSockAddr, true);

        // Fill in the appropriate fields
        SocketAddresses[0].lpSockaddr = pSockAddr;
        SocketAddresses[0].iSockaddrLength = Marshal.SizeOf(sockAddr);

        // Get the site name for this address
        result = DsAddressToSiteNames("domaincontroller.mydomain.com", 1, SocketAddresses, ref pSites);

        if(result != ERROR_SUCCESS)
        {
            throw new Win32Exception(result);
        }

        // Read the string out of memory
        IntPtr pSiteName = Marshal.ReadIntPtr(pSites, 0);

        // If a site could not be found for this address, pSiteName will be 0, so only marshal out the string if
        // we got back a valid pointer.
        if (pSiteName != IntPtr.Zero)
        {
            siteName = Marshal.PtrToStringAuto(pSiteName);
        }

        // Be sure to free the memory allocated
        NetApiBufferFree(pSites);
    }

    return siteName;
}
```
