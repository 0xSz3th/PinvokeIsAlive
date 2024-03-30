
## C# Signature:
```cs
[DllImport("iphlpapi.dll", EntryPoint = "PfBindInterfaceToIPAddress")]
    static extern uint PfBindInterfaceToIPAddress(IntPtr Interface_handle, uint pfatType, ref uint IPAddress);
```

## VB Signature:
```cs
Declare Function PfBindInterfaceToIPAddress Lib "iphlpapi.dll" (TODO) As TODO
```

## Notes:
```cs
/// <summary>
    /// The PfBindInterfaceToIPAddress function associates an interface with the IP stack index having the specified address.
    /// </summary>
    /// <param name="Interface_handle">[in] Specifies a handle to the interface to associate with the IP stack index.</param>
    /// <param name="pfatType">[in] Specifies the address type for the interface. This parameter is of type PFADDRESSTYPE. </param>
    /// <param name="IPAddress">[in] Pointer to an array of bytes that specifies the IP address for the interface.</param>
    /// <returns>If the function succeeds, the return value is NO_ERROR.</returns>
```

## Sample Code:
```cs
using System;
    using System.Collections.Generic;
    using System.Net;
    using System.Runtime.InteropServices;
    using Microsoft.Win32;
```

## Sample Code:
```cs
/// <summary>
    /// IP packet filter management wrapper for Iphlpapi.dll (Win 2000/XP)
    /// </summary>
    class Program
    {
    // C conversions for Fltdefs.h
    internal const int FALSE = 0;
    internal const int TRUE = 1;

    //enums
    internal enum PFFORWARD_ACTION : uint
    {
        PF_ACTION_FORWARD = 0,
        PF_ACTION_DROP
    }

    internal enum PFADDRESSTYPE : uint
    {
        PF_IPV4,
        PF_IPV6
    }

    internal enum PROTOCOL : uint
    {
        ANY = 0x00,
        ICMP = 0x01,
        TCP = 0x06,
        UDP = 0x11
    }

    internal enum FILTER_FLAGS : uint
    {
        FD_FLAGS = 0x1
    }

    [StructLayout(LayoutKind.Sequential, Pack = 1)]
    internal unsafe struct PPF_FILTER_DESCRIPTOR
    {
        public FILTER_FLAGS dwFilterFlags;
        public UInt32 dwRule;
        public PFADDRESSTYPE pfatType;

        public UInt32* SrcAddr;
        public UInt32* SrcMask;
        public UInt32* DstAddr;
        public UInt32* DstMask;

        public PROTOCOL dwProtocol;
        public UInt32 fLateBound;
        public UInt16 wSrcPort;
        public UInt16 wDstPort;
        public UInt16 wSrcPortHighRange;
        public UInt16 wDstPortHighRange;
    }

    static void Main(string[] args)
    {
        string[] hostsToBlock = new string[2];
        hostsToBlock[0] = "67.77.87.97,255.255.255.255,0";    //blocks all traffic on any port to/from 67.77.87.97
        hostsToBlock[1] = "0.0.0.0,0.0.0.0,29000";        //blocks all traffic on port 29000, in and out
        StartPacketFilter(hostsToBlock);
        System.Windows.Forms.Application.Run();
    }

    internal static UInt32 lIpFromString(string sIpAddress)
    {
        UInt32 lIp = 0;
        try
        {
        string[] octets = sIpAddress.Split(new string[] { "." }, StringSplitOptions.None);

        if (octets.Length != 4)
            return 0;

        for (int i = 0; i < 4; i++)
            lIp |= (UInt32.Parse(octets[i]) << (i * 8));
        }
        catch { }
        return lIp;
    }

    internal static string[] GetLocalIpAddresses()
    {
        IPHostEntry host = Dns.GetHostEntry(Dns.GetHostName());
        string[] localIpAddresses = new string[host.AddressList.Length];
        for (int i = 0; i < host.AddressList.Length; i++)
        {
        localIpAddresses[i] = host.AddressList[i].ToString();
        }
        return localIpAddresses;
    }

    internal static bool StartPacketFilter(string[] hosts)
    {
        string[] localIpAddresses = GetLocalIpAddresses();
        if (localIpAddresses == null)
        return false;

        foreach (string localAddress in localIpAddresses)
        {
        uint result;
        IntPtr interfaceHandle = new IntPtr();

        //convert the string IP to an unsigned int for p/invoke
        UInt32 lLocalIp = lIpFromString(localAddress);

        //create a filter interface in the tcp/ip stack
        result = IpPacketFilter.PfCreateInterface(0, PFFORWARD_ACTION.PF_ACTION_FORWARD, PFFORWARD_ACTION.PF_ACTION_FORWARD, FALSE, TRUE, ref interfaceHandle);
        if (result != 0)
            return false;

        //bind interface to an ip address
        result = IpPacketFilter.PfBindInterfaceToIPAddress(interfaceHandle, PFADDRESSTYPE.PF_IPV4, ref lLocalIp);
        if (result != 0)
            return false;

        foreach (string targetHost in hosts)
        {
            IntPtr filterHandle = new IntPtr();
            string[] hostDetail = targetHost.Split(new string[] { "," }, StringSplitOptions.None);
            if (hostDetail != null && hostDetail.Length == 3)
            {
            //build the filter structure
            PPF_FILTER_DESCRIPTOR filter = new PPF_FILTER_DESCRIPTOR();
            filter.dwFilterFlags = FILTER_FLAGS.FD_FLAGS;
            filter.dwRule = FALSE;
            filter.pfatType = PFADDRESSTYPE.PF_IPV4;
            filter.dwProtocol = PROTOCOL.TCP;

            uint iSrcAddr = lLocalIp;
            uint iSrcMask = lIpFromString("255.255.255.255");
            filter.wSrcPort = 0;
            filter.wSrcPortHighRange = 0;

            uint iDstAddr = lIpFromString(hostDetail[0]);
            uint iDstMask = lIpFromString(hostDetail[1]);
            filter.wDstPort = UInt16.Parse(hostDetail[2]);
            filter.wDstPortHighRange = UInt16.Parse(hostDetail[2]);

            unsafe
            {
                filter.SrcAddr = &iSrcAddr;
                filter.DstAddr = &iDstAddr;
                filter.SrcMask = &iSrcMask;
                filter.DstMask = &iDstMask;
            }
            // add filter to interface (both inbound and outbound)
            result = IpPacketFilter.PfAddFiltersToInterface(interfaceHandle, 1, ref filter, 1, ref filter, filterHandle);
            if (result != 0)
                return false;
            }
        }
        }
        return true;
    }
    }
```
