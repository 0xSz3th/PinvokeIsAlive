
## C# Signature:
```cs
[DllImport("dhcpsapi.dll", SetLastError = true, CharSet = CharSet.Unicode)] 
public static extern uint DhcpEnumSubnets( 
    string ServerIpAddress, 
    ref uint ResumeHandle, 
    uint PreferredMaximum, 
    out IntPtr EnumInfo, 
    ref uint ElementsRead, 
    ref uint ElementsTotal 
);
```

## VB Signature:
```cs
Declare Unicode Function DhcpEnumSubnets Lib "Dhcpsapi" (ByVal ServerIpAddress As String, ByRef ResumeHandle As Integer, ByVal PreferredMaximum As Integer, ByRef EnumInfo As IntPtr, ByRef ElementsRead As Integer, ByRef ElementsTotal As Integer) As Integer
```

## Sample Code:
```cs
static void Main() 
{ 
    String ServerIpAddress = "192.168.0.250"; 
    UInt32 DHCPResult = 0; 

    IntPtr ips; 
    uint nr = 0; 
    uint total = 0; 
    uint resumeHandle = 0; 

    DHCPResult = DhcpEnumSubnets(ServerIpAddress, ref resumeHandle, 1000, out ips, ref nr, ref total); 
    if (DHCPResult == 0) 
    { 

       DHCP_IP_ARRAY ipArray = (DHCP_IP_ARRAY)Marshal.PtrToStructure(ips, typeof(DHCP_IP_ARRAY)); 

       int size = (int)ipArray.NumElements; 
       IntPtr outArray = ipArray.IPAddresses; 
       DHCP_IP_ADDRESS[] ipAddressArray = new DHCP_IP_ADDRESS[size]; 
       IntPtr current = outArray; 
       for (int i = 0; i < size; i++) 
       { 
      ipAddressArray[i] = new DHCP_IP_ADDRESS(); 
      Marshal.PtrToStructure(current, ipAddressArray[i]); 
      Marshal.DestroyStructure(current, typeof(DHCP_IP_ADDRESS)); 
      current = (IntPtr)((int)current + Marshal.SizeOf(ipAddressArray[i])); 

      Console.WriteLine("{0}", UInt32IPAddressToString(ipAddressArray[i].IPAddress)); 
       } 
       Marshal.FreeCoTaskMem(outArray);

       Console.WriteLine("Elements read {0} of total {1}", nr, total); 
    } 
    else 
    { 
       int code = 0; 
       unchecked 
       { 
      code = (int)DHCPResult; 
       } 
       Win32Exception winex = new Win32Exception(code); 
       Console.WriteLine(winex.NativeErrorCode + " : " + winex.Message); 
    } 
} 

[DllImport("dhcpsapi.dll", SetLastError = true, CharSet = CharSet.Unicode)] 
public static extern uint DhcpEnumSubnets( 
    string ServerIpAddress, 
    ref uint ResumeHandle, 
    uint PreferredMaximum, 
    out IntPtr EnumInfo, 
    ref uint ElementsRead, 
    ref uint ElementsTotal 
); 

[StructLayout(LayoutKind.Sequential)] 
public struct DHCP_IP_ARRAY 
{ 
    public uint NumElements; 
    public IntPtr IPAddresses; 
} 

/// This is a custom type/class 
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi)] 
public class DHCP_IP_ADDRESS 
{ 
    public UInt32 IPAddress; 
} 

public static string UInt32IPAddressToString(UInt32 ipAddress) 
{ 
    IPAddress ipA = new IPAddress(ipAddress); 
    string[] sIp = ipA.ToString().Split('.'); 

    return sIp[3] + "." + sIp[2] + "." + sIp[1] + "." + sIp[0]; 
}
```
