
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError = true, BestFitMapping = false, ThrowOnUnmappableChar = true)]
[return: MarshalAs(UnmanagedType.Bool)]
internal static extern bool LogonUser(
  [MarshalAs(UnmanagedType.LPStr)] string pszUserName,
  [MarshalAs(UnmanagedType.LPStr)] string pszDomain,
  [MarshalAs(UnmanagedType.LPStr)] string pszPassword,
  int dwLogonType,
  int dwLogonProvider,
  ref IntPtr phToken);
```

## VB .NET Signature:
```cs
Declare Auto Function LogonUser Lib "advapi32.dll" (ByVal lpszUsername As String, _
   ByVal lpszDomain As String, ByVal lpszPassword As String, ByVal dwLogonType As LogonType, _
    ByVal dwLogonProvider As LogonProvider, ByRef phToken As IntPtr) As Integer
```

## VB .NET Signature:
```cs
<DllImport("advapi32.dll", SetLastError:=true)> _
   Public Function LogonUser( ByVal lpszUsername as String, _
     ByVal lpszDomain As String, ByVal lpszPassword As String, ByVal dwLogonType As LogonType, _
     ByVal dwLogonProvider As LogonProvider, ByRef phToken As IntPtr) As Integer
   End Function
```

## User-Defined Types:
```cs
Public Enum LogonType As Integer
    'This logon type is intended for users who will be interactively using the computer, such as a user being logged on 
    'by a terminal server, remote shell, or similar process.
    'This logon type has the additional expense of caching logon information for disconnected operations; 
    'therefore, it is inappropriate for some client/server applications,
    'such as a mail server.
    LOGON32_LOGON_INTERACTIVE = 2

    'This logon type is intended for high performance servers to authenticate plaintext passwords.
    'The LogonUser function does not cache credentials for this logon type.
    LOGON32_LOGON_NETWORK = 3

    'This logon type is intended for batch servers, where processes may be executing on behalf of a user without 
    'their direct intervention. This type is also for higher performance servers that process many plaintext
    'authentication attempts at a time, such as mail or Web servers. 
    'The LogonUser function does not cache credentials for this logon type.
    LOGON32_LOGON_BATCH = 4

    'Indicates a service-type logon. The account provided must have the service privilege enabled. 
    LOGON32_LOGON_SERVICE = 5

    'This logon type is for GINA DLLs that log on users who will be interactively using the computer. 
    'This logon type can generate a unique audit record that shows when the workstation was unlocked. 
    LOGON32_LOGON_UNLOCK = 7

    'This logon type preserves the name and password in the authentication package, which allows the server to make 
    'connections to other network servers while impersonating the client. A server can accept plaintext credentials 
    'from a client, call LogonUser, verify that the user can access the system across the network, and still 
    'communicate with other servers.
    'NOTE: Windows NT:  This value is not supported. 
    LOGON32_LOGON_NETWORK_CLEARTEXT = 8

    'This logon type allows the caller to clone its current token and specify new credentials for outbound connections.
    'The new logon session has the same local identifier but uses different credentials for other network connections. 
    'NOTE: This logon type is supported only by the LOGON32_PROVIDER_WINNT50 logon provider.
    'NOTE: Windows NT:  This value is not supported. 
    LOGON32_LOGON_NEW_CREDENTIALS = 9
    End Enum

    Public Enum LogonProvider As Integer
    'Use the standard logon provider for the system. 
    'The default security provider is negotiate, unless you pass NULL for the domain name and the user name 
    'is not in UPN format. In this case, the default provider is NTLM. 
    'NOTE: Windows 2000/NT:   The default security provider is NTLM.
    LOGON32_PROVIDER_DEFAULT = 0
    LOGON32_PROVIDER_WINNT35 = 1
    LOGON32_PROVIDER_WINNT40 = 2
    LOGON32_PROVIDER_WINNT50 = 3
    End Enum
```

## C# User-Defined Types
```cs
public enum LogonType
    {
        /// <summary>
        /// This logon type is intended for users who will be interactively using the computer, such as a user being logged on  
        /// by a terminal server, remote shell, or similar process.
        /// This logon type has the additional expense of caching logon information for disconnected operations; 
        /// therefore, it is inappropriate for some client/server applications,
        /// such as a mail server.
        /// </summary>
        LOGON32_LOGON_INTERACTIVE = 2,

        /// <summary>
        /// This logon type is intended for high performance servers to authenticate plaintext passwords.

        /// The LogonUser function does not cache credentials for this logon type.
        /// </summary>
        LOGON32_LOGON_NETWORK = 3,

        /// <summary>
        /// This logon type is intended for batch servers, where processes may be executing on behalf of a user without 
        /// their direct intervention. This type is also for higher performance servers that process many plaintext
        /// authentication attempts at a time, such as mail or Web servers. 
        /// The LogonUser function does not cache credentials for this logon type.
        /// </summary>
        LOGON32_LOGON_BATCH = 4,

        /// <summary>
        /// Indicates a service-type logon. The account provided must have the service privilege enabled. 
        /// </summary>
        LOGON32_LOGON_SERVICE = 5,

        /// <summary>
        /// This logon type is for GINA DLLs that log on users who will be interactively using the computer. 
        /// This logon type can generate a unique audit record that shows when the workstation was unlocked. 
        /// </summary>
        LOGON32_LOGON_UNLOCK = 7,

        /// <summary>
        /// This logon type preserves the name and password in the authentication package, which allows the server to make 
        /// connections to other network servers while impersonating the client. A server can accept plaintext credentials 
        /// from a client, call LogonUser, verify that the user can access the system across the network, and still 
        /// communicate with other servers.
        /// NOTE: Windows NT:  This value is not supported. 
        /// </summary>
        LOGON32_LOGON_NETWORK_CLEARTEXT = 8,

        /// <summary>
        /// This logon type allows the caller to clone its current token and specify new credentials for outbound connections.
        /// The new logon session has the same local identifier but uses different credentials for other network connections. 
        /// NOTE: This logon type is supported only by the LOGON32_PROVIDER_WINNT50 logon provider.
        /// NOTE: Windows NT:  This value is not supported. 
        /// </summary>
        LOGON32_LOGON_NEW_CREDENTIALS = 9,
    }

    public enum LogonProvider
    {
        /// <summary>
        /// Use the standard logon provider for the system. 
        /// The default security provider is negotiate, unless you pass NULL for the domain name and the user name 
        /// is not in UPN format. In this case, the default provider is NTLM. 
        /// NOTE: Windows 2000/NT:   The default security provider is NTLM.
        /// </summary>
        LOGON32_PROVIDER_DEFAULT = 0,
        LOGON32_PROVIDER_WINNT35 = 1,
        LOGON32_PROVIDER_WINNT40 = 2,
        LOGON32_PROVIDER_WINNT50 = 3
    }
```

## Sample Code:
```cs
const int LOGON32_LOGON_INTERACTIVE       = 2;
const int LOGON32_LOGON_NETWORK       = 3;
const int LOGON32_LOGON_BATCH         = 4;
const int LOGON32_LOGON_SERVICE       = 5;
const int LOGON32_LOGON_UNLOCK        = 7;
const int LOGON32_LOGON_NETWORK_CLEARTEXT = 8;
const int LOGON32_LOGON_NEW_CREDENTIALS   = 9;

const int LOGON32_PROVIDER_DEFAULT    = 0; 
IntPtr hToken;
IntPtr hTokenDuplicate;

if (LogonUser(username, domain, password,
     LOGON32_LOGON_INTERACTIVE, LOGON32_PROVIDER_DEFAULT, out hToken))
{
     if (DuplicateToken(hToken, 2, out hTokenDuplicate))
     {
     WindowsIdentity windowsIdentity = new WindowsIdentity(hTokenDuplicate);
     WindowsImpersonationContext impersonationContext = windowsIdentity.Impersonate();
    // ...
     impersonationContext.Undo();   
     }
}

if (hToken != IntPtr.Zero) CloseHandle(hToken);
if (hTokenDuplicate != IntPtr.Zero) CloseHandle(hTokenDuplicate);
```

## Sample Code:
```cs
private static WindowsIdentity LogonUserTCPListen(string userName, string domain, string password)
     {
        // need a full duplex stream - loopback is easiest way to get that
        TcpListener tcpListener = new TcpListener(IPAddress.Loopback, 0);
        tcpListener.Start();
        ManualResetEvent done = new ManualResetEvent(false);

        WindowsIdentity id = null;
        tcpListener.BeginAcceptTcpClient(delegate(IAsyncResult asyncResult)
        {
        try
        {
            using (NegotiateStream serverSide = new NegotiateStream(
                 tcpListener.EndAcceptTcpClient(asyncResult).GetStream()))
            {
            serverSide.AuthenticateAsServer(CredentialCache.DefaultNetworkCredentials,
                 ProtectionLevel.None, TokenImpersonationLevel.Impersonation);
            id = (WindowsIdentity)serverSide.RemoteIdentity;
            }
        }
        catch
        { id = null; }
        finally
        { done.Set(); }
        }, null);

        using (NegotiateStream clientSide = new NegotiateStream(new TcpClient("localhost",
             ((IPEndPoint)tcpListener.LocalEndpoint).Port).GetStream()))
        {
        try
        {
            clientSide.AuthenticateAsClient(new NetworkCredential(userName, password, domain),
             "", ProtectionLevel.None, TokenImpersonationLevel.Impersonation);
        }
        catch
        { id = null; }//When the authentication fails it throws an exception
        }
        tcpListener.Stop();
        done.WaitOne();//Wait until we really have the id populated to continue
        return id;
     }
```

## Sample Code in VB.NET:
```cs
Private m_tcpListener As TcpListener

    Private m_winid As WindowsIdentity
    Private m_done As ManualResetEvent
    Private Function LogonUserTCPListen(ByVal userName As String, ByVal domain As String, ByVal password As String) As WindowsIdentity

        ' need a full duplex stream - loopback is easiest way to get that
        m_tcpListener = New TcpListener(IPAddress.Loopback, 0)
        m_tcpListener.Start()
        m_done = New ManualResetEvent(false)

        m_winid = Nothing

        m_tcpListener.BeginAcceptTcpClient(AddressOf TCPListenerCallBack, Nothing)

        Try

        Dim localEndpoint As IPEndPoint = DirectCast(m_tcpListener.LocalEndpoint, IPEndPoint)
        Using clientSide As New NegotiateStream(New TcpClient("localhost", localEndpoint.Port).GetStream())

            clientSide.AuthenticateAsClient(New NetworkCredential(userName, password, domain), _
                    "", ProtectionLevel.None, TokenImpersonationLevel.Impersonation)
        End Using
        Catch ex As Exception
        m_winid = Nothing
        End Try
        m_tcpListener.Stop()
        m_done.WaitOne()//Wait until we really have the id populated to continue
        Return m_winid
    End Function

    Private Sub TCPListenerCallBack(ByVal asyncResult As IAsyncResult)
        Try

        Using serverSide As New NegotiateStream(m_tcpListener.EndAcceptTcpClient(asyncResult).GetStream())

            serverSide.AuthenticateAsServer(CredentialCache.DefaultNetworkCredentials, _
                ProtectionLevel.None, _
                TokenImpersonationLevel.Impersonation)

            m_winid = DirectCast(serverSide.RemoteIdentity, WindowsIdentity)
        End Using

        Catch
        m_winid = Nothing
        Finally
        m_done.Set()
        End Try
    End Sub
```
