
## C# Signature:
```cs
[DllImport("iphlpapi.dll", ExactSpelling=true)]
  public static extern int SendARP( 
      uint DestIP, uint SrcIP, byte[] pMacAddr, ref int PhyAddrLen);
```

## VB Signature:
```cs
Declare Function SendARP Lib "iphlpapi.dll" (
      ByVal DestIP As UInt32, ByVal SrcIP As UInt32, _
      ByVal pMacAddr As Byte(), ByRef PhyAddrLen As Integer) As Integer
```

## Sample Code:
```cs
Public Shared Function GetMAC(ByVal IPAddress A

    Dim addr As IPAddress = IPAddress.Parse(IPAddress)
    Dim mac() As Byte = New Byte(6) {}
    Dim len As Integer = mac.Length
    SendARP(CType(addr.Address, UInt32), 0, mac, len)
    Dim macAddress As String = BitConverter.ToString(mac, 0, len)
    Return macAddress

End Function
```

## Sample Code:
```cs
IPAddress dst = IPAddress.Parse(

// Please do not use the IPAddress.Address property
// This API is now obsolete. --> http://msdn.microsoft.com/en-us/library/system.net.ipaddress.address.aspx
// to get the IP in Integer mode use

uint uintAddress = BitConverter.ToUInt32(dst.GetAddressBytes(), 0);
byte[] macAddr = new byte[6];
int macAddrLen = macAddr.Length;
int retValue = SendARP(uintAddress, 0, macAddr, ref macAddrLen);
if (retValue != 0) {
    throw new Win32Exception(retValue, "SendARP failed.");
}

string[] str = new string[(int)macAddrLen];
for (int i = 0; i < macAddrLen; i++)
    str[i] = macAddr[i].ToString("x2");

Console.WriteLine(string.Join(":", str));
```

## Alternative Managed API:
```cs
Public Shared Function GetMAC(ByVal IPAddresse As String) As String

    Dim macAddress = ""
    Dim dst As IPAddress = Net.IPAddress.Parse(IPAddresse)
    Dim uintAddress = BitConverter.ToUInt32(dst.GetAddressBytes(), 0)
    Dim macAddr() As Byte = New Byte(6) {}
    Dim macAddrLen As Integer = macAddr.Length
    Dim retValue = SendARP(uintAddress, 0, macAddr, macAddrLen)
    Dim str(macAddrLen) ' = New String(macAddrLen).ToString
    For i = 0 To macAddrLen - 1
         macAddress = macAddress & macAddr(i).ToString("x2") & ":"
    Next
    macAddress = Mid(macAddress, 1, Len(macAddress) - 1)
    Return macAddress
    End Function
Send ARP message to a Network Card in the LAN4/28/2022 2:04:00 AM - -217.237.84.5TODO - a short description of this collection of constants4/6/2012 12:59:20 AM - anonymous
```
