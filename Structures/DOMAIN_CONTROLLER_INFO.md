
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
struct DOMAIN_CONTROLLER_INFO 
{
    [MarshalAs(UnmanagedType.LPTStr)]
    public string    DomainControllerName;
    [MarshalAs(UnmanagedType.LPTStr)]
    public string    DomainControllerAddress;
    public uint    DomainControllerAddressType;
    public Guid    DomainGuid;
    [MarshalAs(UnmanagedType.LPTStr)]
    public string    DomainName;
    [MarshalAs(UnmanagedType.LPTStr)]
    public string    DnsForestName;
    public uint        Flags;
    [MarshalAs(UnmanagedType.LPTStr)]
    public string    DcSiteName;
    [MarshalAs(UnmanagedType.LPTStr)]
    public string    ClientSiteName;
}
```

## VB Definition:
```cs
Structure DOMAIN_CONTROLLER_INFO 
   Public TODO
End Structure
```
