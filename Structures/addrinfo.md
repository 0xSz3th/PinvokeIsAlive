
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
    internal unsafe struct addrinfo
    {
        internal AI ai_flags;
        internal ADDRESS_FAMILIES_INT ai_family;
        internal SOCKET_TYPE_INT ai_socktype;
        internal PROTOCOL_INT ai_protocol;
        internal uint ai_addrlen;

        //internal IntPtr ai_canonname;
        internal char* ai_canonname;

        //internal IntPtr ai_addr;
        internal sockaddr_UNSAFE* ai_addr;

        //internal IntPtr ai_next;
        internal addrinfo* ai_next;

        internal string[] Hosts
        {
        get
        {
            var hostList = new List<string>();
            var addressList = new List<addrinfo> {this};
            addressList.AddRange(Children);

            foreach (var info in addressList)
            {
            try
            {
                hostList.Add(info.SockaddrIn6.Host);
            }
            catch
            {
            }
            }

            return hostList.ToArray();
        }
        }

        internal addrinfo[] Children
        {
        get
        {
            if ((IntPtr) ai_next == IntPtr.Zero)
            return new addrinfo[0];

            var info = ai_next;
            var childList = new List<addrinfo>();

            while (true)
            {
            childList.Add(*info);

            if ((IntPtr) (info->ai_next) == IntPtr.Zero)
                break;
            info = info->ai_next;
            }
            return childList.ToArray();
        }
        }

        internal string Name
        {
        get { return new string(ai_canonname); }
        }

        internal sockaddr_in SockaddrIn
        {
        get
        {
            return (sockaddr_in) Marshal.PtrToStructure(
            (IntPtr) ai_addr,
            typeof (sockaddr_in));
        }
        }

        internal sockaddr_in6 SockaddrIn6
        {
        get
        {
            return (sockaddr_in6) Marshal.PtrToStructure(
            (IntPtr) ai_addr,
            typeof (sockaddr_in6));
        }
        }

        internal static addrinfo CreateHints()
        {
        return new addrinfo()
               {
                   ai_flags = AI.AI_NOTHING,
                   ai_family = ADDRESS_FAMILIES_INT.AF_UNSPEC,
                   ai_socktype = SOCKET_TYPE_INT.SOCK_STREAM,
                   ai_protocol = PROTOCOL_INT.IPPROTO_IP
               };
        }

        internal static addrinfo FromPtr(IntPtr handle)
        {
        return *(addrinfo*) handle;
        }
    }
```

## VB Definition:
```cs
Structure addrinfo 
   Public TODO
End Structure
```
