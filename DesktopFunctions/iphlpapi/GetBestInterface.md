
## C# Signature:
```cs
[DllImport("iphlpapi.dll", SetLastError=true)]
static extern int GetBestInterface(UInt32 DestAddr, out UInt32 BestIfIndex);
```

## VB Signature:
```cs
Declare Function GetBestInterface Lib "iphlpapi.dll" (TODO) As TODO
```

## Sample Code:
```cs
public static class Win32ApiCalls
    {
    [DllImport("iphlpapi.dll", CharSet = CharSet.Auto)]
    public static extern int GetBestInterface(UInt32 destAddr, out UInt32 bestIfIndex);
    }

    class Program
    {
    static void Main(string[] args)
    {
        try
        {
        IPHostEntry hostInfo = Dns.GetHostEntry("www.yahoo.com");

        Console.WriteLine("Host name : " + hostInfo.HostName);
        Console.WriteLine("\r\nAliases : ");

        foreach (var thisAlias in hostInfo.Aliases)
        {
            Console.WriteLine(thisAlias);
        }
        Console.WriteLine("\r\nIP Address list :");
        foreach (var thisAddress in hostInfo.AddressList)
        {
            Console.WriteLine(thisAddress);
        }
        IPAddress ipv4Address = (from thisAddress in hostInfo.AddressList
                     where thisAddress.AddressFamily == AddressFamily.InterNetwork
                     select thisAddress).FirstOrDefault();
        if (ipv4Address == null)
        {
            Console.WriteLine("No Ipv4 address found for www.yahoo.com.");
            return;
        }

        Console.WriteLine("\r\nGetting best interface to reach {0}...", ipv4Address);

        UInt32 ipv4AddressAsUInt32 = BitConverter.ToUInt32(ipv4Address.GetAddressBytes(), 0);
        UInt32 interfaceindex;
        int result = Win32ApiCalls.GetBestInterface(ipv4AddressAsUInt32, out interfaceindex);
        if (result != 0)
        {
            throw new Win32Exception(result);
        }
        NetworkInterface interfaceInfo = GetNetworkInterfaceByIndex(interfaceindex);
        Console.WriteLine("Best interface:\r\n" +
                  " Index {0}\r\n" +
                  " Description: {1}\r\n" +
                  " Id: {2}", interfaceindex, interfaceInfo.Description, interfaceInfo.Id);
        }
        catch (SocketException e)
        {
        Console.WriteLine("SocketException caught!!!");
        Console.WriteLine("Source : " + e.Source);
        Console.WriteLine("Message : " + e.Message);
        }
        catch (ArgumentNullException e)
        {
        Console.WriteLine("ArgumentNullException caught!!!");
        Console.WriteLine("Source : " + e.Source);
        Console.WriteLine("Message : " + e.Message);
        }
        catch (NullReferenceException e)
        {
        Console.WriteLine("NullReferenceException caught!!!");
        Console.WriteLine("Source : " + e.Source);
        Console.WriteLine("Message : " + e.Message);
        }
        catch (Win32Exception e)
        {
        Console.WriteLine("Win32Exception caught!!!");
        Console.WriteLine("Source : " + e.Source);
        Console.WriteLine("Message : " + e.Message);
        }
        catch (Exception e)
        {
        Console.WriteLine("Exception caught!!!");
        Console.WriteLine("Source : " + e.Source);
        Console.WriteLine("Message : " + e.Message);
        }
    }

    private static NetworkInterface GetNetworkInterfaceByIndex(uint index)
    {
        // Search in all network interfaces that support IPv4.
        NetworkInterface ipv4Interface = (from thisInterface in NetworkInterface.GetAllNetworkInterfaces()
                          where thisInterface.Supports(NetworkInterfaceComponent.IPv4)
                          let ipv4Properties = thisInterface.GetIPProperties().GetIPv4Properties()
                          where ipv4Properties != null && ipv4Properties.Index == index
                          select thisInterface).SingleOrDefault();
        if (ipv4Interface != null)
        return ipv4Interface;

        // Search in all network interfaces that support IPv6.
        NetworkInterface ipv6Interface = (from thisInterface in NetworkInterface.GetAllNetworkInterfaces()
                          where thisInterface.Supports(NetworkInterfaceComponent.IPv6)
                          let ipv6Properties = thisInterface.GetIPProperties().GetIPv6Properties()
                          where ipv6Properties != null && ipv6Properties.Index == index
                          select thisInterface).SingleOrDefault();

        return ipv6Interface;
    }
    }
```
