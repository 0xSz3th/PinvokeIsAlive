
## C# Signature:
```cs
[DllImport("dhcpsapi.dll", SetLastError = true, CharSet = CharSet.Auto)]
public static extern uint DhcpEnumSubnetClients(
    string ServerIpAddress,
    uint SubnetAddress,
    ref uint ResumeHandle,
    uint PreferredMaximum,
    out IntPtr ClientInfo,
    ref uint ElementsRead,
    ref uint ElementsTotal);
```

## VB Signature:
```cs
Declare Unicode Function DhcpEnumSubnetClients Lib "Dhcpsapi" (ByVal ServerIpAddress As String, ByVal SubnetAddress As Integer, ByRef ResumeHandle As Integer, ByVal PreferredMaximum As Integer, ByRef ClientInfo As IntPtr, ByRef ClientsRead As Integer, ByRef ClientsTotal As Integer) As Integer
```

## Sample Code:
```cs
Imports System.Runtime.InteropServices
```

## Sample Code:
```cs
Declare Unicode Function DhcpEnumSubnetClients Lib "dhcpsapi" (ByVal ServerIpAddress As String, ByVal SubnetAddress As Int32, ByRef ResumeHandle As IntPtr, ByVal PreferredMaximum As Integer, ByRef ClientInfo As IntPtr, ByRef ClientsRead As Integer, ByRef ClientsTotal As Integer) As Integer

    <StructLayout(LayoutKind.Sequential)> _
    Private Structure DHCP_IP_ARRAY
    Dim NumElements As Int32
    Dim Elements As IntPtr
    End Structure

    <StructLayout(LayoutKind.Sequential)> _
   Private Structure DHCP_CLIENT_INFO_ARRAY

    Dim NumElements As Integer
    Dim Clients As IntPtr

    End Structure

    <StructLayout(LayoutKind.Sequential)> _
Private Structure DHCP_CLIENT_INFO

    Dim ClientIpAddress As Int32
    Dim SubnetMask As Int32
    Dim ClientHardwareAddress As DHCP_BINARY_DATA

    <MarshalAs(UnmanagedType.LPWStr)> _
        Dim ClientName As String

    <MarshalAs(UnmanagedType.LPWStr)> _
    Dim ClientComment As String

    Dim ClientLeaseExpires As Date_Time
    Dim OwnerHost As DHCP_HOST_INFO

    End Structure

    <StructLayout(LayoutKind.Sequential)> _
    Private Structure DHCP_BINARY_DATA
    Dim DataLength As Int32
    Dim Data As IntPtr
    End Structure

    <StructLayout(LayoutKind.Sequential)> _
   Private Structure Date_Time

    <MarshalAs(UnmanagedType.U4)> _
    Dim dwLowDateTime As UInt32

    <MarshalAs(UnmanagedType.U4)> _
    Dim dwHighDateTime As UInt32

    End Structure

    <StructLayout(LayoutKind.Sequential)> _
Private Structure DHCP_HOST_INFO

    Dim IpAddress As Int32

    <MarshalAs(UnmanagedType.LPWStr)> _
    Dim NetBiosName As String

    <MarshalAs(UnmanagedType.LPWStr)> _
    Dim HostName As String

    End Structure

public sub ListSubnetClients()

        Dim Client_Array As DHCP_CLIENT_INFO_ARRAY
        Dim DHCP_Clients() As DHCP_CLIENT_INFO
```

## Sample Code:
```cs
Dim i,j As Int16

        Dim pt As IntPtr

        Dim Read_Clients, Total_Clients As Int32
        Dim Error_Code As Int32
        Dim Rem_Handle As IntPtr
        Dim Scope_I As Int32

'Scope_I = "10.0.3.0"
        Scope_I = 167772928    

        'Call dhcpsapi
        Error_Code = DhcpEnumSubnetClients(DHCP_Server, Scope_I, Rem_Handle, 65537, pt, Read_Clients, Total_Clients)
```

## Sample Code:
```cs
Client_Array = Marshal.PtrToStructure(pt, GetType(DHCP_CLIENT_INFO_ARRAY))

        ReDim DHCP_Clients(Client_Array.NumElements - 1)

       For i = 0 To Client_Array.NumElements - 1
        pt = Marshal.ReadIntPtr(Client_Array.Clients, j)
        DHCP_Clients(i) = Marshal.PtrToStructure(pt, GetType(DHCP_CLIENT_INFO))
        pt = IntPtr.Zero
        j = j + 4
        Next i

end sub
```

## Sample Code:
```cs
using System;
using System.Collections.Generic;
using System.Text;
using System.Runtime.InteropServices;
using System.ComponentModel;
using System.Xml;
using System.Net;

namespace dhcp_enum_clients
{
    public struct CUSTOM_CLIENT_INFO
    {
    public string ClientName;
    public string IpAddress;
    public string MacAddress;
    }

    [StructLayout(LayoutKind.Sequential)]
    public struct DHCP_CLIENT_INFO_ARRAY
    {
    public uint NumElements;
    public IntPtr Clients;
    }

    [StructLayout(LayoutKind.Sequential)]
    public struct DHCP_CLIENT_UID
    {
    public uint DataLength;
    public IntPtr Data;
    }

    [StructLayout(LayoutKind.Sequential)]
    public struct DATE_TIME
    {
    public uint dwLowDateTime;
    public uint dwHighDateTime;

    public DateTime Convert()
    {
        if (dwHighDateTime== 0 && dwLowDateTime == 0)
        {
        return DateTime.MinValue;
        }
        if (dwHighDateTime == int.MaxValue && dwLowDateTime == UInt32.MaxValue)
        {
        return DateTime.MaxValue;
        }
        return DateTime.FromFileTime((((long) dwHighDateTime) << 32) | (UInt32) dwLowDateTime);
    }
    }

    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
    public struct DHCP_HOST_INFO
    {
    public uint IpAddress;
    public string NetBiosName;
    public string HostName;
    }

    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
    public struct DHCP_CLIENT_INFO
    {
    public uint ClientIpAddress;
    public uint SubnetMask;
    public DHCP_CLIENT_UID ClientHardwareAddress; //no pointer -> structure !!
    [MarshalAs(UnmanagedType.LPWStr)]
    public string ClientName;
    [MarshalAs(UnmanagedType.LPWStr)]
    public string ClientComment;
    public DATE_TIME ClientLeaseExpires; //no pointer -> structure !!
    public DHCP_HOST_INFO OwnerHost; //no pointer -> structure
    }

    class Program
    {
    static void Main()
    {
        enum_clients("192.168.0.254", "192.168.0.0");
    }
```

## Sample Code:
```cs
static void enum_clients(string Server, string Subnet)
    {
        string ServerIpAddress = Server;
        uint Response = 0;
        uint SubnetMask = StringIPAddressToUInt32(Subnet);
        IntPtr info_array_ptr;
        uint ResumeHandle = 0;
        uint nr_clients_read = 0;
        uint nr_clients_total = 0;

        Response = DhcpEnumSubnetClients(ServerIpAddress, SubnetMask, ref ResumeHandle,
           65536, out info_array_ptr, ref nr_clients_read, ref nr_clients_total);

        DHCP_CLIENT_INFO_ARRAY clients = (DHCP_CLIENT_INFO_ARRAY)Marshal.PtrToStructure(info_array_ptr, typeof(DHCP_CLIENT_INFO_ARRAY));
        Console.WriteLine(clients.NumElements.ToString());
        int size = (int)clients.NumElements;
        IntPtr[] ptr_array = new IntPtr[size];
        IntPtr current = clients.Clients;
        for (int i = 0; i < size; i++)
        {
        ptr_array[i] = Marshal.ReadIntPtr(current);
        current = (IntPtr)((int)current + (int)Marshal.SizeOf(typeof(IntPtr)));
        }
        CUSTOM_CLIENT_INFO[] clients_array = new CUSTOM_CLIENT_INFO[size];
        for (int i = 0; i < size; i++)
        {
        DHCP_CLIENT_INFO curr_element = (DHCP_CLIENT_INFO)Marshal.PtrToStructure(ptr_array[i], typeof(DHCP_CLIENT_INFO));
        clients_array[i].IpAddress = UInt32IPAddressToString(curr_element.ClientIpAddress);
        clients_array[i].ClientName = curr_element.ClientName;
        clients_array[i].MacAddress = String.Format("{0:x2}-{1:x2}-{2:x2}-{3:x2}-{4:x2}-{5:x2}",
            Marshal.ReadByte(curr_element.ClientHardwareAddress.Data),
            Marshal.ReadByte(curr_element.ClientHardwareAddress.Data, 1),
            Marshal.ReadByte(curr_element.ClientHardwareAddress.Data, 2),
            Marshal.ReadByte(curr_element.ClientHardwareAddress.Data, 3),
            Marshal.ReadByte(curr_element.ClientHardwareAddress.Data, 4),
            Marshal.ReadByte(curr_element.ClientHardwareAddress.Data, 5));

        //This section will throw an AccessViolationException
        // Marshal.DestroyStructure(current, typeof(DHCP_CLIENT_INFO));
        // current = (IntPtr)((int)current + (int)Marshal.SizeOf(curr_element));
        //Replace with:
        Marshal.DestroyStructure(ptr_array[i], typeof(DHCP_CLIENT_INFO));
        }
        Console.WriteLine("");
    }

    public static uint StringIPAddressToUInt32(string ip_string)
    {
        IPAddress IpA = System.Net.IPAddress.Parse(ip_string);
        byte[] ip_bytes = IpA.GetAddressBytes();
        uint ip_uint = (uint)ip_bytes[0] << 24;
        ip_uint += (uint)ip_bytes[1] << 16;
        ip_uint += (uint)ip_bytes[2] << 8;
        ip_uint += (uint)ip_bytes[3];
        return ip_uint;
    }

    public static string UInt32IPAddressToString(uint ipAddress)
    {
        IPAddress ipA = new IPAddress(ipAddress);
        string[] sIp = ipA.ToString().Split('.');

        return sIp[3] + "." + sIp[2] + "." + sIp[1] + "." + sIp[0];
    }

    [DllImport("dhcpsapi.dll", SetLastError = true, CharSet = CharSet.Auto)]
    public static extern uint DhcpEnumSubnetClients(
        string ServerIpAddress,
        uint SubnetAddress,
        ref uint ResumeHandle,
        uint PreferredMaximum,
        out IntPtr ClientInfo,
        ref uint ElementsRead,
        ref uint ElementsTotal
    );

    }
}
```
