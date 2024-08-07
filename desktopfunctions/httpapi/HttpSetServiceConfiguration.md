
## C# Signature:
```cs
[DllImport("httpapi.dll", SetLastError = true)]
static extern uint HttpSetServiceConfiguration(
     IntPtr ServiceIntPtr,
     HTTP_SERVICE_CONFIG_ID ConfigId,
     IntPtr pConfigInformation,
     int ConfigInformationLength,
     IntPtr pOverlapped);
```

## VB Signature:
```cs
Declare Function HttpSetServiceConfiguration Lib "httpapi.dll" (ByVal mustbezero As IntPtr, ByVal configID As Integer, ByVal configInfo As HTTP_SERVICE_CONFIG_URLACL_SET, ByVal configInfoLength As Integer, ByVal mustBeZero2 As IntPtr) As Integer
```

## Sample Code:
```cs
void ReserveURL(string networkURL, string securityDescriptor)
{
     uint retVal = (uint) ErrorCodes.NOERROR; // NOERROR = 0

     retVal = HttpApi.HttpInitialize(HttpApi.HTTPAPI_VERSION, HttpApi.HTTP_INITIALIZE_CONFIG, IntPtr.Zero);
     if ((uint) ErrorCodes.NOERROR == retVal)
     {
     HTTP_SERVICE_CONFIG_URLACL_KEY keyDesc = new HTTP_SERVICE_CONFIG_URLACL_KEY(networkURL);
     HTTP_SERVICE_CONFIG_URLACL_PARAM paramDesc = new HTTP_SERVICE_CONFIG_URLACL_PARAM(securityDescriptor);

     HTTP_SERVICE_CONFIG_URLACL_SET inputConfigInfoSet = new HTTP_SERVICE_CONFIG_URLACL_SET();
     inputConfigInfoSet.KeyDesc = keyDesc;
     inputConfigInfoSet.ParamDesc = paramDesc;

     IntPtr pInputConfigInfo = Marshal.AllocCoTaskMem(Marshal.SizeOf(typeof(HTTP_SERVICE_CONFIG_URLACL_SET)));
     Marshal.StructureToPtr(inputConfigInfoSet, pInputConfigInfo, false);

     retVal = HttpApi.HttpSetServiceConfiguration(IntPtr.Zero,
         HTTP_SERVICE_CONFIG_ID.HttpServiceConfigUrlAclInfo,
         pInputConfigInfo,
         Marshal.SizeOf(inputConfigInfoSet),
         IntPtr.Zero);

     if ((uint) ErrorCodes.ERROR_ALREADY_EXISTS == retVal)  // ERROR_ALREADY_EXISTS = 183
     {
         retVal = HttpApi.HttpDeleteServiceConfiguration(IntPtr.Zero,
         HTTP_SERVICE_CONFIG_ID.HttpServiceConfigUrlAclInfo,
         pInputConfigInfo,
         Marshal.SizeOf(inputConfigInfoSet),
         IntPtr.Zero);

         if ((uint) ErrorCodes.NOERROR == retVal)
         {
         retVal = HttpApi.HttpSetServiceConfiguration(IntPtr.Zero,
             HTTP_SERVICE_CONFIG_ID.HttpServiceConfigUrlAclInfo,
             pInputConfigInfo,
             Marshal.SizeOf(inputConfigInfoSet),
             IntPtr.Zero);
         }
     }

     Marshal.FreeCoTaskMem(pInputConfigInfo);
     HttpApi.HttpTerminate(HttpApi.HTTP_INITIALIZE_CONFIG, IntPtr.Zero);
     }

     if ((uint) ErrorCodes.NOERROR != retVal)
     {
     throw new Win32Exception(Convert.ToInt32(retVal));
     }
}
```

## Sample Code:
```cs
class SetSSLCert
    {
    #region DllImport

    [DllImport("httpapi.dll", SetLastError = true)]
    public static extern uint HttpInitialize(
        HTTPAPI_VERSION Version,
        uint Flags,
        IntPtr pReserved);

    [DllImport("httpapi.dll", SetLastError = true)]
    static extern uint HttpSetServiceConfiguration(
         IntPtr ServiceIntPtr,
         HTTP_SERVICE_CONFIG_ID ConfigId,
         IntPtr pConfigInformation,
         int ConfigInformationLength,
         IntPtr pOverlapped);

    [DllImport("httpapi.dll", SetLastError = true)]
    static extern uint HttpDeleteServiceConfiguration(
        IntPtr ServiceIntPtr,
        HTTP_SERVICE_CONFIG_ID ConfigId,
        IntPtr pConfigInformation,
        int ConfigInformationLength,
        IntPtr pOverlapped);

    [DllImport("httpapi.dll", SetLastError = true)]
    public static extern uint HttpTerminate(
        uint Flags,
        IntPtr pReserved);

    enum HTTP_SERVICE_CONFIG_ID
    {
        HttpServiceConfigIPListenList = 0,
        HttpServiceConfigSSLCertInfo,
        HttpServiceConfigUrlAclInfo,
        HttpServiceConfigMax
    }

    [StructLayout(LayoutKind.Sequential)]
    public struct HTTP_SERVICE_CONFIG_IP_LISTEN_PARAM
    {
        public ushort AddrLength;
        public IntPtr pAddress;
    }

    [StructLayout(LayoutKind.Sequential)]
    struct HTTP_SERVICE_CONFIG_SSL_SET
    {
         public HTTP_SERVICE_CONFIG_SSL_KEY KeyDesc;
         public HTTP_SERVICE_CONFIG_SSL_PARAM ParamDesc;
    }

    [StructLayout(LayoutKind.Sequential)]
    public struct HTTP_SERVICE_CONFIG_SSL_KEY
    {
        public IntPtr pIpPort;
    }

    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
    struct HTTP_SERVICE_CONFIG_SSL_PARAM
    {
        public int SslHashLength;
        public IntPtr pSslHash;
        public Guid AppId;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string pSslCertStoreName;
        public uint DefaultCertCheckMode;
        public int DefaultRevocationFreshnessTime;
        public int DefaultRevocationUrlRetrievalTimeout;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string pDefaultSslCtlIdentifier;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string pDefaultSslCtlStoreName;
        public uint DefaultFlags;
    }

    [StructLayout(LayoutKind.Sequential, Pack = 2)]
    public struct HTTPAPI_VERSION
    {
        public ushort HttpApiMajorVersion;
        public ushort HttpApiMinorVersion;

        public HTTPAPI_VERSION(ushort majorVersion, ushort minorVersion)
        {
        HttpApiMajorVersion = majorVersion;
        HttpApiMinorVersion = minorVersion;
        }
    }

    #endregion 

    #region Constants

    public const uint HTTP_INITIALIZE_CONFIG = 0x00000002;
    public const uint HTTP_SERVICE_CONFIG_SSL_FLAG_USE_DS_MAPPER = 0x00000001;
    public const uint HTTP_SERVICE_CONFIG_SSL_FLAG_NEGOTIATE_CLIENT_CERT = 0x00000002;
    public const uint HTTP_SERVICE_CONFIG_SSL_FLAG_NO_RAW_FILTER = 0x00000004;
    private static int NOERROR = 0;
    private static int ERROR_ALREADY_EXISTS = 183;

    #endregion 

    #region Public methods

    public static void BindCertificate(string ipAddress, int port, byte[] hash)
    {
        uint retVal = (uint)NOERROR; // NOERROR = 0
```

## Sample Code:
```cs
HTTPAPI_VERSION httpApiVersion = new HTTPAPI_VERSION(1, 0);
        retVal = HttpInitialize(httpApiVersion, HTTP_INITIALIZE_CONFIG, IntPtr.Zero);
        if ((uint)NOERROR == retVal)
        {
        HTTP_SERVICE_CONFIG_SSL_SET configSslSet = new HTTP_SERVICE_CONFIG_SSL_SET();
        HTTP_SERVICE_CONFIG_SSL_KEY httpServiceConfigSslKey = new HTTP_SERVICE_CONFIG_SSL_KEY();
        HTTP_SERVICE_CONFIG_SSL_PARAM configSslParam = new HTTP_SERVICE_CONFIG_SSL_PARAM();

        IPAddress ip = IPAddress.Parse(ipAddress);

        IPEndPoint ipEndPoint = new IPEndPoint(ip, port);
        // serialize the endpoint to a SocketAddress and create an array to hold the values.  Pin the array.
        SocketAddress socketAddress = ipEndPoint.Serialize();
        byte[] socketBytes = new byte[socketAddress.Size];
        GCHandle handleSocketAddress = GCHandle.Alloc(socketBytes, GCHandleType.Pinned);
        // Should copy the first 16 bytes (the SocketAddress has a 32 byte buffer, the size will only be 16,
        //which is what the SOCKADDR accepts
        for (int i = 0; i < socketAddress.Size; ++i)
        {
            socketBytes[i] = socketAddress[i];
        }

        httpServiceConfigSslKey.pIpPort = handleSocketAddress.AddrOfPinnedObject();

        GCHandle handleHash = GCHandle.Alloc(hash, GCHandleType.Pinned);
        configSslParam.AppId = Guid.NewGuid();
        configSslParam.DefaultCertCheckMode = 0;
        configSslParam.DefaultFlags = HTTP_SERVICE_CONFIG_SSL_FLAG_NEGOTIATE_CLIENT_CERT;
        configSslParam.DefaultRevocationFreshnessTime = 0;
        configSslParam.DefaultRevocationUrlRetrievalTimeout = 0;
        configSslParam.pSslCertStoreName = StoreName.My.ToString();
        configSslParam.pSslHash = handleHash.AddrOfPinnedObject(); 
        configSslParam.SslHashLength = hash.Length;
        configSslSet.ParamDesc = configSslParam;
        configSslSet.KeyDesc = httpServiceConfigSslKey;

        IntPtr pInputConfigInfo = Marshal.AllocCoTaskMem(Marshal.SizeOf(typeof(HTTP_SERVICE_CONFIG_SSL_SET)));
        Marshal.StructureToPtr(configSslSet, pInputConfigInfo, false);

        retVal = HttpSetServiceConfiguration(IntPtr.Zero,
            HTTP_SERVICE_CONFIG_ID.HttpServiceConfigSSLCertInfo,
            pInputConfigInfo,
            Marshal.SizeOf(configSslSet),
            IntPtr.Zero);

        if ((uint)ERROR_ALREADY_EXISTS == retVal)  // ERROR_ALREADY_EXISTS = 183
        {
            retVal = HttpDeleteServiceConfiguration(IntPtr.Zero,
            HTTP_SERVICE_CONFIG_ID.HttpServiceConfigSSLCertInfo,
            pInputConfigInfo,
            Marshal.SizeOf(configSslSet),
            IntPtr.Zero);

            if ((uint)NOERROR == retVal)
            {
            retVal = HttpSetServiceConfiguration(IntPtr.Zero,
                HTTP_SERVICE_CONFIG_ID.HttpServiceConfigSSLCertInfo,
                pInputConfigInfo,
                Marshal.SizeOf(configSslSet),
                IntPtr.Zero);
            }
        }

        handleSocketAddress.Free();
        handleHash.Free();
        Marshal.FreeCoTaskMem(pInputConfigInfo);
        HttpTerminate(HTTP_INITIALIZE_CONFIG, IntPtr.Zero);
        }

        if ((uint)NOERROR != retVal)
        {
        throw new Win32Exception(Convert.ToInt32(retVal));
        }
    }

    #endregion 
    }
```
