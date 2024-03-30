
## C# Signature:
```cs
[DllImport("dhcpsapi.dll", SetLastError = true, CharSet = CharSet.Unicode)]
static extern uint DhcpRemoveSubnetElementV5(
    string ServerIpAddress,
    uint SubnetAddress,
    ref DHCP_SUBNET_ELEMENT_DATA_V5 RemoveElementInfo,
    DHCP_FORCE_FLAG ForceFlag);
```

## User-Defined Types:
```cs
const uint ERROR_SUCCESS = 0;

[StructLayout(LayoutKind.Sequential)]
struct DHCP_SUBNET_ELEMENT_DATA_V5 {
    public DHCP_SUBNET_ELEMENT_TYPE ElementType;
    public IntPtr ElementValue;
}

[StructLayout(LayoutKind.Sequential)]
struct DHCP_IP_RESERVATION_V4 {
    public uint ReservedIpAddress;
    public IntPtr ReservedForClient;
    public DHCP_CLIENT_TYPE bAllowedClientTypes;
}

[StructLayout(LayoutKind.Sequential)]
struct DHCP_BINARY_DATA {
    public uint DataLength;
    public IntPtr Data;
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

enum DHCP_CLIENT_TYPE : byte {
    CLIENT_TYPE_DHCP,
    CLIENT_TYPE_BOOTP,
    CLIENT_TYPE_BOTH
}

enum DHCP_FORCE_FLAG : uint {
    DhcpFullForce,
    DhcpNoForce
}
```

## Sample Code:
```cs
static List<IntPtr> _allocations = new List<IntPtr>();

static IntPtr AllocStructure(object structure) {
    IntPtr result = Marshal.AllocHGlobal(Marshal.SizeOf(structure));
    Marshal.StructureToPtr(structure, result, false);
    _allocations.Add(result);
    return result;
}

static IntPtr AllocByteArray(byte[] array) {
    IntPtr result = Marshal.AllocHGlobal(array.Length);
    Marshal.Copy(array, 0, result, array.Length);
    _allocations.Add(result);
    return result;
}

static void Free() {
    foreach (IntPtr allocation in _allocations)
        Marshal.FreeHGlobal(allocation);

    _allocations.Clear();
}

void RemoveReservedIp(byte[] hardwareAddress, uint address) {
    NativeMethods.DHCP_BINARY_DATA uid = new NativeMethods.DHCP_BINARY_DATA();
    uid.Data = AllocByteArray(hardwareAddress);
    uid.DataLength = (uint) hardwareAddress.Length;

    NativeMethods.DHCP_IP_RESERVATION_V4 reservation = new NativeMethods.DHCP_IP_RESERVATION_V4();
    reservation.ReservedIpAddress = address;
    reservation.ReservedForClient = AllocStructure(uid);
    reservation.bAllowedClientTypes = NativeMethods.DHCP_CLIENT_TYPE.CLIENT_TYPE_BOTH;

    NativeMethods.DHCP_SUBNET_ELEMENT_DATA_V5 element = new NativeMethods.DHCP_SUBNET_ELEMENT_DATA_V5();
    element.ElementType = NativeMethods.DHCP_SUBNET_ELEMENT_TYPE.DhcpReservedIps;
    element.ElementValue = AllocStructure(reservation);

    try {
        uint result = NativeMethods.DhcpRemoveSubnetElementV5(server.Address, subnet, ref element, NativeMethods.DHCP_FORCE_FLAG.DhcpFullForce);
        if (result != NativeMethods.ERROR_SUCCESS)
            throw new DhcpException(result, "DhcpRemoveSubnetElementV5");
        }
        finally {
            Free();
        }
    }
}
```
