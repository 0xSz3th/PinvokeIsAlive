
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Ansi)]
public struct IP_ADAPTER_INFO
{
    public IntPtr Next;
    public Int32 ComboIndex;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst=MAX_ADAPTER_NAME_LENGTH + 4)]
      public string AdapterName;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst=MAX_ADAPTER_DESCRIPTION_LENGTH + 4)]
      public string AdapterDescription;
    public UInt32 AddressLength;
    [MarshalAs(UnmanagedType.ByValArray, SizeConst=MAX_ADAPTER_ADDRESS_LENGTH)]
      public byte [] Address;
    public Int32 Index;
    public UInt32 Type;
    public UInt32 DhcpEnabled;
    public IntPtr CurrentIpAddress;
    public IP_ADDR_STRING IpAddressList;
    public IP_ADDR_STRING GatewayList;
    public IP_ADDR_STRING DhcpServer;
    public bool HaveWins;
    public IP_ADDR_STRING PrimaryWinsServer;
    public IP_ADDR_STRING SecondaryWinsServer;
    public Int32 LeaseObtained;
    public Int32 LeaseExpires;
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Ansi)> _
Public Class IP_ADAPTER_INFO
    Public [Next] As IntPtr
    Public ComboIndex As Int32
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=(MAX_ADAPTER_NAME_LENGTH + 4))> _
    Public AdapterName As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=(MAX_ADAPTER_DESCRIPTION_LENGTH + 4))> _
    Public AdapterDescription As String
    Public AddressLength As Int32
    <MarshalAs(UnmanagedType.ByValArray, SizeConst:=(MAX_ADAPTER_ADDRESS_LENGTH))> _
    Public Address() As Byte
    Public Index As Int32
    Public Type As Int32
    Public DhcpEnabled As Int32
    Public CurrentIpAddress As Int32
    Public IpAddressList As IP_ADDR_STRING
    Public GatewayList As IP_ADDR_STRING
    Public DhcpServer As IP_ADDR_STRING
    Public HaveWins As Int32
    Public PrimaryWinsServer As IP_ADDR_STRING
    Public SecondaryWinsServer As IP_ADDR_STRING
    Public LeaseObtained As Int32
    Public LeaseExpires As Int32
End Class
```
