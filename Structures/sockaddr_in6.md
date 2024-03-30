
## C# Definition:
```cs
internal struct sockaddr_in6
    {
        [FieldOffset(0)] internal ADDRESS_FAMILIES sin6_family;
        [FieldOffset(2)] internal ushort sin6_port;
        [FieldOffset(4)] internal uint sin6_flowinfo;
        [FieldOffset(8)] internal in6_addr sin6_addr;
        [FieldOffset(24)] internal uint sin6_scope_id;

        internal string Host
        {
        get
        {
            var local = this;
            var length = (uint) 256;
            var builder = new StringBuilder((int) length);

            var data = new WSAData();
            WSAStartup(2, ref data);
            WSAAddressToString(ref local, (uint) Marshal.SizeOf(local), IntPtr.Zero, builder,
                          ref length);
            WSACleanup();

            return builder.ToString().Split(':')[0];
        }

        }

        internal string Port
        {
        get
        {
            var local = this;
            var length = (uint) 256;
            var builder = new StringBuilder((int) length);

            var data = new WSAData();
            WSAStartup(2, ref data);
            WSAAddressToString(ref local, (uint) Marshal.SizeOf(local), IntPtr.Zero, builder,
                          ref length);
            WSACleanup();

            return builder.ToString().Split(':')[1];
        }

        }

        internal static sockaddr_in6 FromString(string host, int port)
        {
        var sockaddr = new sockaddr_in6();
        var lpAddressLength = Marshal.SizeOf(sockaddr);
        WSAStringToAddress(host + ":" + port, EnumLib.ADDRESS_FAMILIES.AF_INET6, IntPtr.Zero,
                          ref sockaddr, ref lpAddressLength);
        return sockaddr;
        }
    }

    [StructLayout(LayoutKind.Explicit, Size = 28)]
    internal struct sockaddr_in6_UNSAFE
    {
        [FieldOffset(0)] internal EnumLib.ADDRESS_FAMILIES sin6_family;
        [FieldOffset(2)] internal ushort sin6_port;
        [FieldOffset(4)] internal uint sin6_flowinfo;
        [FieldOffset(8)] internal in6_addr sin6_addr;
        [FieldOffset(24)] internal uint sin6_scope_id;

        internal string Host
        {
        get
        {
            var local = this;
            var length = (uint) 256;
            var builder = new StringBuilder((int) length);

            var data = new WSAData();
            WSAStartup(2, ref data);
            WSAAddressToString(ref local, (uint) Marshal.SizeOf(local), IntPtr.Zero, builder,
                          ref length);
            WSACleanup();

            return builder.ToString().Split(':')[0];
        }

        }

        internal string Port
        {
        get
        {
            var local = this;
            var length = (uint) 256;
            var builder = new StringBuilder((int) length);

            var data = new WSAData();
            WSAStartup(2, ref data);
            WSAAddressToString(ref local, (uint) Marshal.SizeOf(local), IntPtr.Zero, builder,
                          ref length);
            WSACleanup();

            return builder.ToString().Split(':')[1];
        }

        }

        internal static sockaddr_in6 FromString(string host, int port)
        {
        var sockaddr = new sockaddr_in6();
        var lpAddressLength = Marshal.SizeOf(sockaddr);
        WSAStringToAddress(host + ":" + port, EnumLib.ADDRESS_FAMILIES.AF_INET6, IntPtr.Zero,
                          ref sockaddr, ref lpAddressLength);
        return sockaddr;
        }
    }
```

## VB Definition:
```cs
Structure sockaddr_in6 
   Public TODO
End Structure
```
