
## C# Signature:
```cs
[DllImport("ntdsapi.dll", CharSet = CharSet.Auto)]
public static extern uint DsGetDomainControllerInfo(
     IntPtr hDs, 
     string DomainName, 
     uint InfoLevel, 
     out uint InfoCount, 
     out IntPtr pInf
);
```

## VB Signature:
```cs
TODO
```

## Sample Code:
```cs
using System;
    using System.Runtime.InteropServices;

    class NtdsHelper
    {
    [DllImport("ntdsapi.dll", CharSet = CharSet.Auto)]
    static public extern uint DsBind(
        string DomainControllerName, 
        string DnsDomainName, out IntPtr phDS
    );

    [DllImport("ntdsapi.dll", CharSet = CharSet.Auto)]
    static public extern uint DsUnBind(ref IntPtr phDS);

    [StructLayout(LayoutKind.Sequential)]
    public struct GUID
    {
        public int a;
        public short b;
        public short c;
        [MarshalAs(UnmanagedType.ByValArray, SizeConst = 8)]
        public byte[] d;
    }

    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
    public struct DS_DOMAIN_CONTROLLER_INFO_2
    {
        [MarshalAs(UnmanagedType.LPTStr)]
        public string NetbiosName;        // SDBAD10004
        [MarshalAs(UnmanagedType.LPTStr)]
        public string DnsHostName;        // sdbad10004.dom1.ad.sys
        [MarshalAs(UnmanagedType.LPTStr)]
        public string SiteName;           // BAD1
        [MarshalAs(UnmanagedType.LPTStr)]
        public string SiteObjectName;     // CN=BAD1,CN=Sites,CN=Configuration,DC=ad,DC=sys
        [MarshalAs(UnmanagedType.LPTStr)]
        public string ComputerObjectName;     // CN=SDBAD10004,OU=Domain Controllers,DC=dom1,DC=ad,DC=sys
        [MarshalAs(UnmanagedType.LPTStr)]
        public string ServerObjectName;       // CN=SDBAD10004,CN=Servers,CN=BAD1,CN=Sites,CN=Configuration,DC=ad,DC=sys   
        [MarshalAs(UnmanagedType.LPTStr)]
        public string NtdsDsaObjectName;      // CN=NTDS Settings,CN=SDBAD10004,CN=Servers,CN=BAD1,CN=Sites,CN=Configuration,DC=ad,DC=sys
        [MarshalAs(UnmanagedType.Bool)]
        public bool fIsPdc;
        [MarshalAs(UnmanagedType.Bool)]
        public bool fDsEnabled;
        [MarshalAs(UnmanagedType.Bool)]
        public bool fIsGc;
        public GUID SiteObjectGuid;
        public GUID ComputerObjectGuid;
        public GUID ServerObjectGuid;
        public GUID NtdsDsaObjectGuid;
    }

    [DllImport("ntdsapi.dll", CharSet = CharSet.Auto)]
    public static extern uint DsGetDomainControllerInfo(
        IntPtr hDs, 
        string DomainName, 
        uint InfoLevel, 
        out uint InfoCount, 
        out IntPtr pInf);

    [DllImport("ntdsapi.dll", CharSet = CharSet.Auto)]
    public static extern void DsFreeDomainControllerInfo(
        uint InfoLevel, 
        uint cInfo, 
        IntPtr pInf);

    }
```

## Sample Code:
```cs
class Program
    {
    static void Main(string[] args)
    {
        Console.WriteLine("binding to domain controllert");
        IntPtr hDC = IntPtr.Zero;
        uint ret = NtdsHelper.DsBind("sdbad10004", "dom1.ad.sys", out hDC);
        if (ret == 0)
        {
        Console.WriteLine("bound... getting infos");

        // this will be our final array of infos... 
        NtdsHelper.DS_DOMAIN_CONTROLLER_INFO_2[] DCinfos;

        IntPtr pDCinfos; // pointer to array of DS_DOMAIN_CONTROLLER_INFO_2
        uint nInfo;     // array length
        ret = NtdsHelper.DsGetDomainControllerInfo(hDC, "dom1.ad.sys", 2, out nInfo, out pDCinfos);
        if (ret == 0)
        {
            Console.WriteLine("we got it...");
            Console.WriteLine("  Number of items returned: " + nInfo.ToString());

            // size our final array 
            DCinfos = new NtdsHelper.DS_DOMAIN_CONTROLLER_INFO_2[nInfo];

            // now copy the system allocated memory to our final (managed) array
            {
            IntPtr pCurrentInfo = pDCinfos;
            NtdsHelper.DS_DOMAIN_CONTROLLER_INFO_2 OneInfo;

            for (uint i = 0; i < nInfo; i++)
            {
                OneInfo = (NtdsHelper.DS_DOMAIN_CONTROLLER_INFO_2)Marshal.PtrToStructure(
                pCurrentInfo, 
                typeof(NtdsHelper.DS_DOMAIN_CONTROLLER_INFO_2)
                );
                DCinfos[i] = OneInfo;   // copy 

                Console.WriteLine(DCinfos[i].NetbiosName);

                // move to next item
                pCurrentInfo = (IntPtr)(
                (int)pCurrentInfo + 
                 Marshal.SizeOf(typeof(NtdsHelper.DS_DOMAIN_CONTROLLER_INFO_2)));
            }
            }

            // important!
            NtdsHelper.DsFreeDomainControllerInfo(2, nInfo, pDCinfos);
        }
        else
            Console.WriteLine("error getting domain infos");

        NtdsHelper.DsUnBind(ref hDC);
        }
        else
        Console.WriteLine("ret: " + ret.ToString());

        Console.ReadLine();
    }
    }
```
