
## C# Signature:
```cs
[DllImport("dhcpsapi.dll", SetLastError = true, CharSet = CharSet.Unicode)]
public static extern uint DhcpEnumSubnetElementsV5(
    string ServerIpAddress,
    uint SubnetAddress,
    DHCP_SUBNET_ELEMENT_TYPE EnumElementType,
    ref uint ResumeHandle,
    uint PreferredMaximum,
    ref IntPtr EnumElementInfo,
    ref uint ElementsRead,
    ref uint ElementsTotal);
```

## User-Defined Types:
```cs
const uint ERROR_SUCCESS = 0;
const uint ERROR_MORE_DATA = 234;
const uint ERROR_NO_MORE_ITEMS = 259;

[StructLayout(LayoutKind.Sequential)]
struct DHCP_SUBNET_ELEMENT_INFO_ARRAY_V5 {
    public uint NumElements;
    public IntPtr Elements;
}

[StructLayout(LayoutKind.Sequential)]
struct DHCP_SUBNET_ELEMENT_DATA_V5 {
    public DHCP_SUBNET_ELEMENT_TYPE ElementType;
    public IntPtr ElementValue;
}

[StructLayout(LayoutKind.Sequential)]
struct DHCP_IP_RANGE {
    public uint StartAddress;
    public uint EndAddress;
}

enum DHCP_SUBNET_ELEMENT_TYPE : uint {
    DhcpIpRanges,
    DhcpSecondaryHosts,
    DhcpReservedIps,
    DhcpExcludedIpRanges,
    DhcpIpRangesDhcpOnly,
    DhcpIpRangesDhcpBootp,
    DhcpIpRangesBootpOnly
}
```

## Sample Code:
```cs
public static List<DhcpIpAddress> GetReservedIps(DhcpServer server, DhcpIpAddress subnet) {
    List<DhcpIpAddress> reservations = new List<DhcpIpAddress>();

    uint resumeHandle = 0;
    uint read = 0, total = 0;
    IntPtr enumInfo = IntPtr.Zero;
    uint result = 0;

    do {
        result = NativeMethods.DhcpEnumSubnetElementsV5(server.Address, subnet, NativeMethods.DHCP_SUBNET_ELEMENT_TYPE.DhcpReservedIps, ref resumeHandle, 1000, ref enumInfo, ref read, ref total);
        if (result == NativeMethods.ERROR_NO_MORE_ITEMS) break;

        if ((result != NativeMethods.ERROR_SUCCESS && result != NativeMethods.ERROR_MORE_DATA) || enumInfo == IntPtr.Zero)
            throw new DhcpException(result, "DhcpEnumSubnetElementsV5");

        NativeMethods.DHCP_SUBNET_ELEMENT_INFO_ARRAY_V5 data;
        data = (NativeMethods.DHCP_SUBNET_ELEMENT_INFO_ARRAY_V5) Marshal.PtrToStructure(enumInfo, typeof(NativeMethods.DHCP_SUBNET_ELEMENT_INFO_ARRAY_V5));

        for (int i = 0; i < data.NumElements; i++) {
            IntPtr p = (IntPtr) ((int) data.Elements + (i * Marshal.SizeOf(typeof(NativeMethods.DHCP_SUBNET_ELEMENT_DATA_V5))));

            NativeMethods.DHCP_SUBNET_ELEMENT_DATA_V5 element;
            element = (NativeMethods.DHCP_SUBNET_ELEMENT_DATA_V5) Marshal.PtrToStructure(p, typeof(NativeMethods.DHCP_SUBNET_ELEMENT_DATA_V5));

            if (element.ElementType == NativeMethods.DHCP_SUBNET_ELEMENT_TYPE.DhcpReservedIps) {
                NativeMethods.DHCP_IP_RESERVATION_V4 reservation;
                reservation = (NativeMethods.DHCP_IP_RESERVATION_V4) Marshal.PtrToStructure(element.ElementValue, typeof(NativeMethods.DHCP_IP_RESERVATION_V4));

                reservations.Add(new DhcpIpAddress(reservation.ReservedIpAddress));
            }
        }
    }
    while (result == NativeMethods.ERROR_MORE_DATA);

    return reservations;
}
```
