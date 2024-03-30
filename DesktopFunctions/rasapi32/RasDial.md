
## C# Signature:
```cs
[DllImport("rasapi32.dll",CharSet=CharSet.Auto)]
static extern uint RasDial([In]RASDIALEXTENSIONS lpRasDialExtensions, [In]string lpszPhonebook, [In]RASDIALPARAMS lpRasDialParams, uint dwNotifierType, Delegate lpvNotifier, ref IntPtr lphRasConn);
```

## VB Signature:
```cs
VB.NET,   :)
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential, Pack = 4)]
    internal struct RASEAPINFO
    {
        public int sizeOfEapData;
        public IntPtr eapData;
    }

    [StructLayout(LayoutKind.Sequential)]
    internal class RASDIALEXTENSIONS 
    { 
        public readonly int dwSize = Marshal.SizeOf(typeof(RASDIALEXTENSIONS));
        public uint dwfOptions = 0;
        public int hwndParent = 0;
        public int reserved = 0;
        public int reserved1 = 0;
        public RASEAPINFO RasEapInfo = new RASEAPINFO();
    }

    [StructLayout(LayoutKind.Sequential,CharSet = CharSet.Auto)]
    internal class RASDIALPARAMS 
    {
        public int dwSize = Marshal.SizeOf(typeof(RASDIALPARAMS));
        [MarshalAs(UnmanagedType.ByValTStr,SizeConst =
            (int) RasFieldSizeConstants.RAS_MaxEntryName+1)]
        public string szEntryName = null; 
        [MarshalAs(UnmanagedType.ByValTStr,SizeConst =
            (int) RasFieldSizeConstants.RAS_MaxPhoneNumber+1)]
        public string szPhoneNumber = null; 
        [MarshalAs(UnmanagedType.ByValTStr,SizeConst =
            (int) RasFieldSizeConstants.RAS_MaxCallbackNumber+1)]
        public string szCallbackNumber = null; 
        [MarshalAs(UnmanagedType.ByValTStr,SizeConst =
            (int) RasFieldSizeConstants.UNLEN+1)]
        public string szUserName = null; 
        [MarshalAs(UnmanagedType.ByValTStr,SizeConst =
            (int) RasFieldSizeConstants.PWLEN+1)]
        public string szPassword = null; 
        [MarshalAs(UnmanagedType.ByValTStr,SizeConst =
            (int) RasFieldSizeConstants.DNLEN+1)]
        public string szDomain = null; 
        public int dwSubEntry = 0;
        public int dwCallbackId = 0;
    }
```
