
## C# Signature:
```cs
using DWORD = System.UInt32;
using ULONG = System.UInt64;

[DllImport(Netapi32, CharSet=CharSet.Auto, SetLastError=true)]
internal static extern DWORD DsGetDcOpen(
     [MarshalAs(UnmanagedType.LPTStr)]
     string DnsName,
     ULONG OptionFlags,
     [MarshalAs(UnmanagedType.LPTStr)]
     string SiteName,
     IntPtr DomainGuid,
     [MarshalAs(UnmanagedType.LPTStr)]
     string DnsForestName,
     ULONG DcFlags,
     out IntPtr RetGetDcContext
     );
```

## C# Signature:
```cs
[DllImport("Netapi32.dll", EntryPoint = "DsGetDcOpenW", CallingConvention = CallingConvention.StdCall, CharSet = CharSet.Unicode)]
internal static extern int DsGetDcOpen(
    [In] string dnsName,
    [In] int optionFlags,
    [In] string siteName,
    [In] IntPtr domainGuid,
    [In] string dnsForestName,
    [In] int dcFlags,
    out IntPtr retGetDcContext
    );
```

## VB Signature:
```cs
Declare Function DsGetDcOpen Lib "netapi32.dll" (TODO) As TODO
```

## Sample Code:
```cs
IntPtr pDcContext = new IntPtr();
    int iReturn = 0;

    // if you are getting the entire domain
    iReturn = DsGetDcOpen("domain1.mydomains.com", 0, null, (System.IntPtr)null, null, 0, out pDcContext);

    // this is a great call, it will give you all the DC's that COVER a site, not just the DC's in that site:
    iReturn = DsGetDcOpen("domain1.mydomains.com", 1, "MYADSITE", (System.IntPtr)null, null, 0, out pDcContext);
```
