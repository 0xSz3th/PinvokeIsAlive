
## C# Signature:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct DHCP_SEARCH_INFO
    {
      public uint SearchType;
      public UInt32 ClientIpAddress;
      public DHCP_BINARY_DATA ClientMacAddress;
      [MarshalAs(UnmanagedType.LPWStr)]
      public string ClientName;

    };
```

## VB Signature:
```cs
<StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Auto)> _
Public Structure DHCP_SEARCH_INFO
     Public SearchType As UInteger
     Public ClientIpAddress As UInt32
     Public ClientMacAddress As DHCP_BINARY_DATA
     <MarshalAs(UnmanagedType.LPWStr)> _
     Public ClientName As String
End Structure
```
