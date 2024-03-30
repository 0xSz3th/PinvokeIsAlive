
## C# Definition:
```cs
public struct RASENTRY
    {
    public int dwSize;
    public uint dwfOptions;
    //
    // Location/phone number.
    //
    public int dwCountryID;
    public int dwCountryCode;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = (int)RASConstants.RAS_MaxAreaCode + 1)]
    public string szAreaCode;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = (int)RASConstants.RAS_MaxPhoneNumber + 1)]
    public string szLocalPhoneNumber;
    public int dwAlternateOffset;
    //
    // PPP/Ip
    //
    public RASIPADDR ipaddr;
    public RASIPADDR ipaddrDns;
    public RASIPADDR ipaddrDnsAlt;
    public RASIPADDR ipaddrWins;
    public RASIPADDR ipaddrWinsAlt;
    //
    // Framing
    //
    public int dwFrameSize;
    public int dwfNetProtocols;
    public int dwFramingProtocol;
    //
    // Scripting
    //
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = (int)RASConstants.MAX_PATH)]
    public string szScript;
    //
    // AutoDial
    //
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = (int)RASConstants.MAX_PATH)]
    public string szAutodialDll;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = (int)RASConstants.MAX_PATH)]
    public string szAutodialFunc;
    //
    // Device
    //
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = (int)RASConstants.RAS_MaxDeviceType + 1)]
    public string szDeviceType;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = (int)RASConstants.RAS_MaxDeviceName + 1)]
    public string szDeviceName;
    //
    // X.25
    //
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = (int)RASConstants.RAS_MaxPadType + 1)]
    public string szX25PadType;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = (int)RASConstants.RAS_MaxX25Address + 1)]
    public string szX25Address;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = (int)RASConstants.RAS_MaxFacilities + 1)]
    public string szX25Facilities;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = (int)RASConstants.RAS_MaxUserData + 1)]
    public string szX25UserData;
    public int dwChannels;
    //
    // Reserved
    //
    public int dwReserved1;
    public int dwReserved2;
```

## C# Definition:
```cs
// 
    // EAP extension type to use
    //
    public int dwCustomAuthKey;
```

## C# Definition:
```cs
//
    // Multilink and BAP
    //
    public int       dwSubEntries;
    public int       dwDialMode;
    public int       dwDialExtraPercent;
    public int       dwDialExtraSampleSeconds;
    public int       dwHangUpExtraPercent;
    public int       dwHangUpExtraSampleSeconds;
    //
    // Idle time out
    //
    public int       dwIdleDisconnectSeconds;
```

## C# Definition:
```cs
public EntryTypes       dwType;
    public EncryptionTypes  dwEncryptionType;
    public int      dwCustomAuthKey;
    public GUID     guidId;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = MAX_PATH)]
    public string       szCustomDialDll;
    public int      dwVpnStrategy;
```

## C# Definition:
```cs
public int      dwfOptions2;
    public int      dwfOptions3;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = (int)RAS_MaxDnsSuffix + 1)]
    public string   szDnsSuffix;
    public int      dwTcpWindowSize;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = MAX_PATH)]
    public string   szPrerequisitePbk;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = (int)RAS_MaxEntryName + 1)]
    public string   szPrerequisiteEntry;
    public int      dwRedialCount;
    public int      dwRedialPause;
```

## C# Definition:
```cs
}
```

## VB Definition:
```cs
Structure RASENTRYNAME 
    Public dwSize As Int32
    Public dwfOptions As Int32
    Public dwCountrylD As Int32
    Public dwCountryCode As Int32
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=RAS_MaxAreaCode + 1)> _
    Public szAreaCode As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=RAS_MaxPhoneNumber + 1)> _
    Public szLocalPhoneNumber As String
    Public dwAlternateOffset As Int32
    Public IPaddr As RASIPADDR
    Public IPaddrDns As RASIPADDR
    Public IPaddrDnsAlt As RASIPADDR
    Public IPaddrWins As RASIPADDR
    Public IPaddrWinsAlt As RASIPADDR
    Public dwFrameSize As Int32
    Public dwNetProtocols As Int32
    Public dwFramingProtocol As Int32
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=MAX_PATH)> _
    Public szScript As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=MAX_PATH)> _
    Public szAutodialDll As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=MAX_PATH)> _
    Public szAutodialFunc As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=RAS_MaxDeviceType + 1)> _
    Public szDeviceType As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=RAS_MaxDeviceName + 1)> _
    Public szDeviceName As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=RAS_MaxPadType + 1)> _
    Public szX25PadType As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=RAS_MaxX25Address + 1)> _
    Public szX25Address As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=RAS_MaxFacilities + 1)> _
    Public szFacilities As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=RAS_MaxUserData + 1)> _
    Public szUserData As String
    Public dwChannels As Int32
    Public dwReservedl As Int32
    Public dwReserved2 As Int32
    Public dwNT4En_SubEntries As Int32
    Public dwNT4En_DialMode As RASDialModes
    Public dwNT4En_DialExtraPercent As Int32
    Public dwNT4En_DialExtraSampleSeconds As Int32
    Public dwNT4En_HangUpExtraPercent As Int32
    Public dwNT4En_HangUpExtraSampleSeconds As Int32
    Public dwNT4En_IdleDisconnectSeconds As Int32
    Public dwType As Int32
    Public dwEncryptionType As Int32
    Public dwCustomAuthKey As Int32
    Public guidId As Guid
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=MAX_PATH)> _
    Public szCustomDialDll As String
    Public dwVpnStrategy As Int32
    Public dwOptions2 As Int32
    Public dwOptions3 As Int32
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=RAS_MaxDnsSuffix)> _
    Public szDNSSuffix As String
    Public dwTcpWindowSize As Int32
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=MAX_PATH)> _
    Public szPrerequisitePbk As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=RAS_MaxEntryName + 1)> _
    Public szPrerequisiteEntry As String
    Public dwRedialCount As Int32
    Public dwRedialPause As Int32
End Structure
```
