
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
struct DS_DOMAIN_CONTROLLER_INFO_2 {
     [MarshalAs(UnmanagedType.LPTStr)] public string NetbiosName;        // server1
     [MarshalAs(UnmanagedType.LPTStr)] public string DnsHostName;        // server1.dom1.ad.sys
     [MarshalAs(UnmanagedType.LPTStr)] public string SiteName;           // Site1
     [MarshalAs(UnmanagedType.LPTStr)] public string SiteObjectName;     // CN=BAD1,CN=Sites,CN=Configuration,DC=ad,DC=sys
     [MarshalAs(UnmanagedType.LPTStr)] public string ComputerObjectName;     // CN=server1,OU=Domain Controllers,DC=dom1,DC=ad,DC=sys
     [MarshalAs(UnmanagedType.LPTStr)] public string ServerObjectName;       // CN=server1,CN=Servers,CN=Site1,CN=Sites,CN=Configuration,DC=ad,DC=sys   
     [MarshalAs(UnmanagedType.LPTStr)] public string NtdsDsaObjectName;      // CN=NTDS Settings,CN=server1,CN=Servers,CN=Site1,CN=Sites,CN=Configuration,DC=ad,DC=sys
     [MarshalAs(UnmanagedType.Bool)] public bool fIsPdc;
     [MarshalAs(UnmanagedType.Bool)] public bool fDsEnabled;
     [MarshalAs(UnmanagedType.Bool)] public bool fIsGc;
     public GUID SiteObjectGuid;
     public GUID ComputerObjectGuid;
     public GUID ServerObjectGuid;
     public GUID NtdsDsaObjectGuid;

}
```

## VB Definition:
```cs
Structure DS_DOMAIN_CONTROLLER_INFO_2 
   Public TODO
End Structure
```
