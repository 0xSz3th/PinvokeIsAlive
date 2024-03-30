
## C# Signature:
```cs
[DllImport("wininet.dll", SetLastError = true, CharSet = CharSet.Auto)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool FtpGetFile(IntPtr hConnect, string remoteFile,
   string newFile, [MarshalAs(UnmanagedType.Bool)] bool failIfExists,
   int flagsAndAttributes, int flags, IntPtr context);
```

## VB Signature:
```cs
Declare Function FtpGetFile Lib "wininet.dll" (ByVal hConnect As IntPtr, _
   ByVal remoteFile As String, ByVal newFile As String, _
   <MarshalAs(UnmanagedType.Bool)> ByVal failIfExists As Boolean, _
   ByVal flagsAndAttributes As Integer, ByVal flags As Integer, _
   ByVal context As IntPtr) As <MarshalAs(UnmanagedType.Bool)> Boolean
```

## Sample Code:
```cs
public class FTPClient
    : IDisposable
    {
    #region Ctors
    public FTPClient()
    {
        FTPPort = INTERNET_DEFAULT_FTP_PORT;
        internetHandle = IntPtr.Zero;
        ftpHandle = IntPtr.Zero;
    }

    ~FTPClient()
    {
        Dispose();
    }
    #endregion

    #region P/Invoke
    [DllImport("wininet.dll", EntryPoint = "InternetConnectW", CharSet = CharSet.Auto, SetLastError = true)]
    private static extern IntPtr InternetConnectW(
        IntPtr hInternet,
        string ServerName,
        ushort ServerPort,
        string sUserName,
        string sPassword,
        uint nService,
        uint nFlags,
        uint nContext);

    [DllImport("wininet.dll", EntryPoint = "InternetOpenW", CharSet = CharSet.Auto, SetLastError = true)]
    public static extern IntPtr InternetOpenW(
        string sAgent,
        uint nAccessType,
        string sProxy,
        string sProxyBypass,
        uint nFlags);

    [DllImport("wininet.dll", EntryPoint = "FtpPutFile")]
    public static extern bool FtpPutFile(
        IntPtr hFtpConn,
        string lpszLocalFile,
        string lpszNewRemoteFile,
        uint dwFlags,
        uint dwContext);

    [DllImport("wininet.dll", EntryPoint = "FtpGetFile", SetLastError = true, CharSet = CharSet.Auto)]
    [return: MarshalAs(UnmanagedType.Bool)]
    private static extern bool FtpGetFile(
        IntPtr hFtpConn,
        string strSource,
        string strTarget,
        [MarshalAs(UnmanagedType.Bool)] bool bFailIfExists,
        uint nFlagsAndAtrribute,
        uint nFlags,
        uint nContext);

    [DllImport("wininet.dll", EntryPoint = "FtpOpenFile", SetLastError = true, CharSet = CharSet.Auto)]
    [return: MarshalAs(UnmanagedType.Bool)]
    private static extern uint FtpOpenFile(
        IntPtr hFtpConn,
        string strFileName,
        uint nAccess,
        uint nFlags,
        uint nContext);

    [DllImport("wininet.dll", EntryPoint = "InternetCloseHandle")]
    public static extern long InternetCloseHandle(IntPtr hInet);

    [DllImport("wininet.dll", EntryPoint = "GetLastError")]
    public static extern long GetLastError();
    #endregion

    #region Members
    private const uint INTERNET_OPEN_TYPE_PRECONFIG = 0;
    private const long INTERNET_OPEN_TYPE_DIRECT = 1;
    private const long INTERNET_OPEN_TYPE_PROXY = 3;
    private const long INTERNET_FLAG_RELOAD = 0x80000000;
    private const ushort INTERNET_DEFAULT_FTP_PORT = 21;
    private const uint INTERNET_FLAG_PASSIVE = 0x08000000;
    private const uint INTERNET_SERVICE_FTP = 1;
    private const uint FILE_ATTRIBUTE_NORMAL = 128;

    private const string IPADDRESS_PATTERN = @"^(([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])\.){3}([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])$";

    private IntPtr internetHandle;

    private IntPtr ftpHandle;
    #endregion

    #region Properties
    public ushort FTPPort { get; set; }

    public string FTPSite { get; set; }

    public string FTPUsername { get; set; }

    public string FTPPassword { get; set; }
    #endregion

    #region Methods
    private void validateFTP()
    {
        if (FTPSite == string.Empty)
        throw new InvalidOperationException(Resources.FTPClient_NoFTPSiteSpecified);
    }

    public void Connect()
    {
        validateFTP();
        if (internetHandle == IntPtr.Zero)
        {
        internetHandle = InternetOpenW("FTPOpen", INTERNET_OPEN_TYPE_PRECONFIG, string.Empty, string.Empty, 0);

        if (internetHandle == IntPtr.Zero)
            throw new Win32Exception(Marshal.GetLastWin32Error());
        }

        if (ftpHandle == IntPtr.Zero)
        {
        ftpHandle = InternetConnectW(internetHandle, FTPSite,
                    FTPPort, FTPUsername, FTPPassword,
                    INTERNET_SERVICE_FTP, INTERNET_FLAG_PASSIVE, 0);

        if (ftpHandle == IntPtr.Zero)
            throw new Win32Exception(Marshal.GetLastWin32Error());
        }
    }

    public void Disconnect()
    {
        try
        {
        if (ftpHandle != IntPtr.Zero)
            InternetCloseHandle(ftpHandle);
        }
        catch
        {
        }
        finally
        {
        ftpHandle = IntPtr.Zero;
        }
        try
        {
        if (internetHandle != IntPtr.Zero)
            InternetCloseHandle(internetHandle);
        }
        catch
        {
        }
        finally
        {
        internetHandle = IntPtr.Zero;
        }
    }

    public void PutFileOnFTPServer(FTPFile file)
    {
        Connect();
        if (!File.Exists(file.SourceFileName))
        throw new InvalidOperationException(Resources.FTPClient_HDSourceFileDoesNotExist);
        if (!FtpPutFile(ftpHandle, file.SourceFileName, file.DesctinationFileName, (uint)file.TransferType, 0))
        throw new Win32Exception(Marshal.GetLastWin32Error());
    }

    public void GetFileFromFTPServer(FTPFile file)
    {
        Connect();
        if (!FtpGetFile(ftpHandle, file.SourceFileName, file.DesctinationFileName, false,
                FILE_ATTRIBUTE_NORMAL, (uint)file.TransferType, 0))
        throw new Win32Exception(Marshal.GetLastWin32Error());
    }

    public void CloseFTP()
    {
        Disconnect();
    }
    #endregion

    #region Inner classes
    public class FTPFile
    {
        #region Ctors
        public FTPFile()
        {
        }

        public FTPFile(string sourceFileName, string destinationFileName, FTPTransferType transferType)
        : this()
        {
        SourceFileName = sourceFileName;
        DesctinationFileName = destinationFileName;
        TransferType = transferType;
        }
        #endregion

        #region Members
        public enum FTPTransferType 
        : uint
        {
        Auto = 0,
        ASCII = 1,
        Binary = 2
        }
        #endregion

        #region Properties
        public string SourceFileName { get; set; }

        public string DesctinationFileName { get; set; }

        public FTPTransferType TransferType { get; set; }
        #endregion

        #region Overrides
        #endregion

        #region Methods
        #endregion
    }
    #endregion

    #region IDisposable Members
    public void Dispose()
    {
        CloseFTP();
        GC.SuppressFinalize(this);
    }

    #endregion
    }
```
