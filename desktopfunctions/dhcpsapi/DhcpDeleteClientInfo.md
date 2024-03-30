
## C# Signature:
```cs
[DllImport("dhcpsapi.dll", SetLastError = true, CharSet = CharSet.Unicode)]
    public static extern int  DhcpDeleteClientInfo(
    string DHCPServer,
    IntPtr ClientInfo);

    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
    public struct DHCP_SEARCH_INFO
    {
        public int DHCPSearchInfoType;
        public UInt32 DHCPIPAddress;
    }
```

## C# Signature:
```cs
public enum  DHCP_SEARCH_INFO_TYPE
    {
        DhcpClientIpAddress,
        DhcpClientHardwareAddress,
        DhcpClientName
    }
```

## VB Signature and sample code:
```cs
Imports System.Runtime.InteropServices
```

## VB Signature and sample code:
```cs
Private Declare Unicode Function DhcpDeleteClientInfo Lib "dhcpsapi.dll" ( _
    ByVal DHCPServer As String, _
    ByVal ClientInfo As Integer) As Integer

    Private Structure DHCP_SEARCH_INFO
    Dim DHCPSearchInfoType As Integer
    Dim DHCPIPAddress As UInt32
    End Structure

    Private Enum DHCP_SEARCH_INFO_TYPE
    DhcpClientIpAddress
    DhcpClientHardwareAddress
    DhcpClientName
    End Enum

   Private Declare Function NetApiBufferAllocate Lib "NETAPI32.DLL" (ByVal ByteCount As Integer, ByRef Buffer As Integer) As Integer

    Private Declare Function NetAPIBufferFree Lib "Netapi32" Alias "NetApiBufferFree" (ByVal lpBuffer As Integer) As Integer
```

## VB Signature and sample code:
```cs
Public Sub DeleteDHCPLease(ByVal IPAddress As String)

    Dim Octets() As String = IPAddress.Split(".")
    Dim HexIP As String

    For Each Octet As String In Octets
        HexIP &= Convert.ToString(Convert.ToInt16(Octet), 16).PadLeft(2, "0")
    Next

    'Dim a As Int32 = Convert.ToInt32(BinaryIP)

    Dim bufptr As Integer
    Dim StructSize As Integer

    Dim ClientInfo As New DHCP_SEARCH_INFO
    ClientInfo.DHCPSearchInfoType = DHCP_SEARCH_INFO_TYPE.DhcpClientIpAddress
    ClientInfo.DHCPIPAddress = Convert.ToUInt32(HexIP, 16)

    StructSize = Marshal.SizeOf(ClientInfo)
    NetApiBufferAllocate(StructSize, bufptr)
    Marshal.StructureToPtr(ClientInfo, IntPtr.op_Explicit(bufptr), True)

    Dim result As Integer = DhcpDeleteClientInfo("nn.nn.nn.nn", bufptr)

    NetAPIBufferFree(bufptr)

    End Sub
```

## Tips & Tricks:
```cs
[DllImport("netapi32.dll", SetLastError = true)]
    public extern static int NetApiBufferFree(IntPtr lpBuffer);

    [DllImport("netapi32.dll", SetLastError = true)]
    public extern static int NetApiBufferAllocate(int ByteCount,ref int Buffer);
```

## Sample Code:
```cs
[DllImport("dhcpsapi.dll", SetLastError = true, CharSet = CharSet.Unicode)]
    public static extern int  DhcpDeleteClientInfo(
    string DHCPServer,
    IntPtr ClientInfo);

    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
    public struct DHCP_SEARCH_INFO
    {
        public int DHCPSearchInfoType;
        public UInt32 DHCPIPAddress;
    }
```

## Sample Code:
```cs
public enum  DHCP_SEARCH_INFO_TYPE
    {
        DhcpClientIpAddress,
        DhcpClientHardwareAddress,
        DhcpClientName
    }

    [DllImport("netapi32.dll", SetLastError = true)]
    public extern static int NetApiBufferFree(IntPtr lpBuffer);

    [DllImport("netapi32.dll", SetLastError = true)]
    public extern static int NetApiBufferAllocate(int ByteCount,ref int Buffer);
```

## Sample Code:
```cs
static extern TODO DhcpDeleteClientInfo(TODO);
static void Main(string[] args)
    {
        //A utility that looks at the dynamic ranges on the following DHCP scopes and deletes the unused dynamic IP reservations
        //(e.g. laptops that have visited the site and have now left before the 5 days lease period). The utility would run during
        //the early hours of the morning against the scopes:- 10.13.25.0, 10.13.27.0, 10.13.107.0 and 10.13.109.0 Laptops that were
        //left connected overnight should have their IP dynamic lease left untouched.
        // Dynamics - 241 to 254

        string scope = "";
        for (int s = 1; s < 5; s++)
        {
        switch (s)
        {
            case 1:
            scope = "10.13.25.";
            break;
            case 2:
            scope = "10.13.27.";
            break;
            case 3:
            scope = "10.13.107.";
            break;
            case 4:
            scope = "10.13.109.";
            break;
        }
         for (int i = 241; i < 255; i++)
        {

            DoWork(scope + i.ToString());
        }
        }
        //Console.Read();
    }
    static void DoWork(string scope)
    {
        // retrieve reservation.
        Ping ping1 = new Ping();
        string SqlServer = "Your SQL Server";
        SqlConnection sqlConnection1 = new SqlConnection("Data Source=" + SqlServer + ";Initial Catalog=DhcpDB;Persist Security Info=True;User ID=user");
        string strSQL = "select * from IP_to_Name where IP_address = '" + scope + "'";
        SqlCommand selCommand = new SqlCommand(strSQL, sqlConnection1);
        selCommand.CommandType = CommandType.Text;
        try
        {
        sqlConnection1.Open();
        SqlDataReader rowReader = selCommand.ExecuteReader();
        while (rowReader.Read())
        {
            //Console.Write("Checking: " + rowReader["IP_address"].ToString());
            PingReply result = ping1.Send(rowReader["IP_address"].ToString(), 1000);
            //Console.WriteLine(" ..........." + result.Status.ToString());
            if (result.Status.ToString() != "Success")
            {
            DoDeletion(rowReader["IP_address"].ToString());
            }
        }
        }

        catch(Exception msg)
        {
        //Console.WriteLine(msg.Message);
        }
        finally
        {
        sqlConnection1.Close();
        ping1.Dispose();
        }
    }

    public static void DoDeletion(string IPAddress)
    {
        string dhcpServer = "n.n.n.n";
        char [] dot = ".".ToCharArray();
        char[] zero = "0".ToCharArray();
        string [] Octets= IPAddress.Split(dot[0]);
    string HexIP = "";

    foreach(string Octet  in Octets)
        {
        HexIP += Convert.ToString(Convert.ToInt16(Octet), 16).PadLeft(2, zero[0]);
        }

        //IntPtr bufptr = IntPtr.Zero;
        int bufptr = 0;
    int StructSize;

    DHCP_SEARCH_INFO ClientInfo = new DHCP_SEARCH_INFO();
    ClientInfo.DHCPSearchInfoType = (int)DHCP_SEARCH_INFO_TYPE.DhcpClientIpAddress;
    ClientInfo.DHCPIPAddress = Convert.ToUInt32(HexIP, 16);

    StructSize = Marshal.SizeOf(ClientInfo);
    NetApiBufferAllocate(StructSize,ref bufptr);
    Marshal.StructureToPtr(ClientInfo, (IntPtr)bufptr, true);

    int result = DhcpDeleteClientInfo(dhcpServer, (IntPtr)bufptr);

    NetApiBufferFree((IntPtr)bufptr);
```

## Sample Code:
```cs
}
    }
```
