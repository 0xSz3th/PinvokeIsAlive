
## C# Signature:
```cs
[DllImport("Netapi32.dll", CharSet=CharSet.Auto, SetLastError=true)]
public static extern int NetServerGetInfo(
    string serverName, 
    int level, 
    out IntPtr pSERVER_INFO_XXX);
```

## VB Signature:
```cs
Declare Function NetServerGetInfo Lib "netapi32.dll" (ByVal ServerName As String, _
    ByVal Level As Integer, ByRef ptrBuff As IntPtr) As Integer
```

## C# User-Defined Types:
```cs
[Flags]
public enum ServerTypes : uint
{
    Workstation = 0x00000001,
    Server = 0x00000002,
    SqlServer = 0x00000004,
    DomainCtrl= 0x00000008,
    BackupDomainCtrl= 0x00000010,
    TimeSource= 0x00000020,
    AppleFilingProtocol = 0x00000040,
    Novell= 0x00000080,
    DomainMember = 0x00000100,
    PrintQueueServer = 0x00000200,
    DialinServer = 0x00000400,
    XenixServer = 0x00000800,
    UnixServer = 0x00000800,
    NT = 0x00001000,
    WindowsForWorkgroups = 0x00002000,
    MicrosoftFileAndPrintServer= 0x00004000,
    NTServer = 0x00008000,
    BrowserService = 0x00010000,
    BackupBrowserService= 0x00020000,
    MasterBrowserService= 0x00040000,
    DomainMaster = 0x00080000,
    OSF1Server = 0x00100000,
    VMSServer = 0x00200000,
    Windows = 0x00400000, 
    DFS = 0x00800000, 
    NTCluster = 0x01000000, 
    TerminalServer= 0x02000000, 
    VirtualNTCluster = 0x04000000, 
    DCE = 0x10000000, 
    AlternateTransport = 0x20000000, 
    LocalListOnly = 0x40000000, 
    PrimaryDomain = 0x80000000,
    All = 0xFFFFFFFF
};

public enum ServerPlatform
{
    DOS = 300,
    OS2 = 400,
    NT = 500,
    OSF = 600,
    VMS = 700
}

[StructLayout(LayoutKind.Sequential)]
public struct SERVER_INFO_100
{
    public ServerPlatform PlatformId;
    [MarshalAs(System.Runtime.InteropServices.UnmanagedType.LPWStr)]
    public string Name;
}

[StructLayout(LayoutKind.Sequential)]
public struct SERVER_INFO_101
{
    public ServerPlatform PlatformId;
    [MarshalAs(UnmanagedType.LPWStr)]
    public string Name;
    public int VersionMajor;
    public int VersionMinor;
    public ServerTypes Type;
    [MarshalAs(UnmanagedType.LPWStr)]
    public string Comment;
}

[StructLayout(LayoutKind.Sequential)]
public struct SERVER_INFO_102
{
    public ServerPlatform PlatformId;
    [MarshalAs(UnmanagedType.LPWStr)]
    public string Name;
    public int VersionMajor;
    public int VersionMinor;
    public ServerTypes Type;
    [MarshalAs(UnmanagedType.LPWStr)]
    public string Comment;
    public int MaxUsers;
    public int AutoDisconnectMinutes;
    [MarshalAs(UnmanagedType.Bool)]
    public bool Hidden;
    public int NetworkAnnounceRate;
    public int NetworkAnnounceRateDelta;
    public int UsersPerLicense;
    [MarshalAs(UnmanagedType.LPWStr)]
    public string UserDirectoryPath;
}
```

## VB.NET User-Defined Types:
```cs
<StructLayout(LayoutKind.Sequential)> _
    Private Structure SERVER_INFO_102
    Dim sv102_platform_id As Integer
    <MarshalAs(UnmanagedType.LPWStr)> Dim sv102_name As String
    Dim sv102_version_major As Integer
    Dim sv102_version_minor As Integer
    Dim sv102_type As Integer
    <MarshalAs(UnmanagedType.LPWStr)> Dim sv102_comment As String
    Dim sv102_users As Integer
    Dim sv102_disc As Integer
    Dim sv102_hidden As Boolean
    Dim sv102_announce As Integer
    Dim sv102_anndelta As Integer
    Dim sv102_licenses As Integer
    <MarshalAs(UnmanagedType.LPWStr)> Dim sv102_userpath As String
    End Structure
```

## VB.NET Sample Code:
```cs
Private Sub GetServerName( )
    Dim ptrBuff As IntPtr
    Dim strServerInfo As SERVER_INFO_102
    Dim lRetCode As Integer
    lRetCode = NetServerGetInfo(vbNullString, 102, ptrBuff)
    strServerInfo = CType(Marshal.PtrToStructure(ptrBuff, GetType(SERVER_INFO_102)), SERVER_INFO_102)
    Debug.WriteLine(strServerInfo.sv102_version_major)
    Debug.WriteLine(strServerInfo.sv102_version_minor)
    End Sub
```

## C# Sample Code (1):
```cs
[DllImport("Netapi32", CharSet = CharSet.Auto, SetLastError = true)]
private static extern int NetServerGetInfo(string serverName, int level, out IntPtr pSERVER_INFO_XXX);

// Wrapper function to allow passing of structure and auto-find of level if structure contains it.
public static T NetServerGetInfo<T>(string serverName = null, int level = 0) where T : struct
{
    if (level == 0)
       level = int.Parse(System.Text.RegularExpressions.Regex.Replace(typeof(T).Name, @"[^\d]", ""));
    IntPtr ptr = IntPtr.Zero;
    try
    {
       int ret = NetServerGetInfo(serverName, level, out ptr);
       if (ret != 0)
      throw new System.ComponentModel.Win32Exception(ret);
       return (T)Marshal.PtrToStructure(ptr, typeof(T));
    }
    finally
    {
       if (ptr != IntPtr.Zero)
      NetApiBufferFree(ptr);
    }
}

public static void Main()
{
    var serverInfo = NetServerGetInfo<SERVER_INFO_101>("SVR0123");
    Console.WriteLine($"Name: {serverInfo.Name}; Version: {serverInfo.VersionMajor}.{serverInfo.VersionMinor}");
}
```

## C# Sample Code (2):
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
private struct DOMAIN_CONTROLLER_INFO 
{
    [MarshalAs(UnmanagedType.LPTStr)]
    public string DomainControllerName;
    [MarshalAs(UnmanagedType.LPTStr)]
    public string DomainControllerAddress;
    public uint DomainControllerAddressType;
    public Guid DomainGuid;
    [MarshalAs(UnmanagedType.LPTStr)]
    public string DomainName;
    [MarshalAs(UnmanagedType.LPTStr)]
    public string DnsForestName;
    public uint Flags;
    [MarshalAs(UnmanagedType.LPTStr)]
    public string DcSiteName;
    [MarshalAs(UnmanagedType.LPTStr)]
    public string ClientSiteName;
} 
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
private struct SERVER_INFO_101
{
    public int PlatformId;
    [MarshalAs(UnmanagedType.LPTStr)]
    public string Name;
    public int VersionMajor;
    public int VersionMinor;
    public int Type;
    [MarshalAs(UnmanagedType.LPTStr)]
    public string Comment;
}

private DOMAIN_CONTROLLER_INFO domainInfo;
private SERVER_INFO_101 serverInfo;

IntPtr pDCI = IntPtr.Zero;
IntPtr pSI = IntPtr.Zero;
try
{
    if(DsGetDcName(null, null, null, null, 0, out pDCI)==0)
    {
        domainInfo = (DOMAIN_CONTROLLER_INFO)Marshal.PtrToStructure(
            pDCI, typeof(DOMAIN_CONTROLLER_INFO));

        if(NetServerGetInfo(domainInfo.DomainControllerName, 101, out pSI)==0)
        {
        serverInfo = (SERVER_INFO_101)Marshal.PtrToStructure(
            pSI, typeof(SERVER_INFO_101));
        }
    }
}
finally
{
    NetApiBufferFree(pDCI);
    NetApiBufferFree(pSI);
}
```
