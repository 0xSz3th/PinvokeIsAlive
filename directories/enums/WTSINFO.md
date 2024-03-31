
## C# Definition:
```cs
/// <summary>
/// Contains values that indicate the type of session information to retrieve in a call to the <see cref="WTSQuerySessionInformation"/> function.
/// </summary>
public enum WtsInfoClass
{
     /// <summary>
     /// A null-terminated string that contains the name of the initial program that Remote Desktop Services runs when the user logs on.
     /// </summary>
     WTSInitialProgram,

     /// <summary>
     /// A null-terminated string that contains the published name of the application that the session is running.
     /// </summary>
     WTSApplicationName,

     /// <summary>
     /// A null-terminated string that contains the default directory used when launching the initial program.
     /// </summary>
     WTSWorkingDirectory,

     /// <summary>
     /// This value is not used.
     /// </summary>
     WTSOEMId,

     /// <summary>
     /// A <B>ULONG</B> value that contains the session identifier.
     /// </summary>
     WTSSessionId,

     /// <summary>
     /// A null-terminated string that contains the name of the user associated with the session.
     /// </summary>
     WTSUserName,

     /// <summary>
     /// A null-terminated string that contains the name of the Remote Desktop Services session. 
     /// </summary>
     /// <remarks>
     /// <B>Note</B>  Despite its name, specifying this type does not return the window station name. 
     /// Rather, it returns the name of the Remote Desktop Services session. 
     /// Each Remote Desktop Services session is associated with an interactive window station. 
     /// Because the only supported window station name for an interactive window station is "WinSta0", 
     /// each session is associated with its own "WinSta0" window station. For more information, see <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms687096(v=vs.85).aspx">Window Stations</see>.
     /// </remarks>
     WTSWinStationName,

     /// <summary>
     /// A null-terminated string that contains the name of the domain to which the logged-on user belongs.
     /// </summary>
     WTSDomainName,

     /// <summary>
     /// The session's current connection state. For more information, see <see cref="WTS_CONNECTSTATE_CLASS"/>.
     /// </summary>
     WTSConnectState,

     /// <summary>
     /// A <B>ULONG</B> value that contains the build number of the client.
     /// </summary>
     WTSClientBuildNumber,

     /// <summary>
     /// A null-terminated string that contains the name of the client.
     /// </summary>
     WTSClientName,

     /// <summary>
     /// A null-terminated string that contains the directory in which the client is installed.
     /// </summary>
     WTSClientDirectory,

     /// <summary>
     /// A <B>USHORT</B> client-specific product identifier.
     /// </summary>
     WTSClientProductId,

     /// <summary>
     /// A <B>ULONG</B> value that contains a client-specific hardware identifier. This option is reserved for future use. 
     /// <see cref="WTSQuerySessionInformation"/> will always return a value of 0.
     /// </summary>
     WTSClientHardwareId,

     /// <summary>
     /// The network type and network address of the client. For more information, see <see cref="WTS_CLIENT_ADDRESS"/>.
     /// </summary>
     /// <remarks>The IP address is offset by two bytes from the start of the <B>Address</B> member of the <see cref="WTS_CLIENT_ADDRESS"/> structure.</remarks>
     WTSClientAddress,

     /// <summary>
     /// Information about the display resolution of the client. For more information, see <see cref="WTS_CLIENT_DISPLAY"/>.
     /// </summary>
     WTSClientDisplay,

     /// <summary>
     /// A USHORT value that specifies information about the protocol type for the session. This is one of the following values:<BR/>
     /// 0 - The console session.<BR/>
     /// 1 - This value is retained for legacy purposes.<BR/>
     /// 2 - The RDP protocol.<BR/>
     /// </summary>
     WTSClientProtocolType,

     /// <summary>
     /// This value returns <B>FALSE</B>. If you call <see cref="GetLastError"/> to get extended error information, <B>GetLastError</B> returns <B>ERROR_NOT_SUPPORTED</B>.
     /// </summary>
     /// <remarks>
     /// <B>Windows Server 2008, Windows Vista, Windows Server 2003, and Windows XP:</B>  This value is not used.
     /// </remarks>
     WTSIdleTime,

     /// <summary>
     /// This value returns <B>FALSE</B>. If you call <see cref="GetLastError"/> to get extended error information, <B>GetLastError</B> returns <B>ERROR_NOT_SUPPORTED</B>.
     /// </summary>
     /// <remarks>
     /// <B>Windows Server 2008, Windows Vista, Windows Server 2003, and Windows XP:</B>  This value is not used.
     /// </remarks>
     WTSLogonTime,

     /// <summary>
     /// This value returns <B>FALSE</B>. If you call <see cref="GetLastError"/> to get extended error information, <B>GetLastError</B> returns <B>ERROR_NOT_SUPPORTED</B>.
     /// </summary>
     /// <remarks>
     /// <B>Windows Server 2008, Windows Vista, Windows Server 2003, and Windows XP:</B>  This value is not used.
     /// </remarks>
     WTSIncomingBytes,

     /// <summary>
     /// This value returns <B>FALSE</B>. If you call <see cref="GetLastError"/> to get extended error information, <B>GetLastError</B> returns <B>ERROR_NOT_SUPPORTED</B>.
     /// </summary>
     /// <remarks>
     /// <B>Windows Server 2008, Windows Vista, Windows Server 2003, and Windows XP:</B>  This value is not used.
     /// </remarks>
     WTSOutgoingBytes,

     /// <summary>
     /// This value returns <B>FALSE</B>. If you call <see cref="GetLastError"/> to get extended error information, <B>GetLastError</B> returns <B>ERROR_NOT_SUPPORTED</B>.
     /// </summary>
     /// <remarks>
     /// <B>Windows Server 2008, Windows Vista, Windows Server 2003, and Windows XP:</B>  This value is not used.
     /// </remarks>
     WTSIncomingFrames,

     /// <summary>
     /// This value returns <B>FALSE</B>. If you call <see cref="GetLastError"/> to get extended error information, <B>GetLastError</B> returns <B>ERROR_NOT_SUPPORTED</B>.
     /// </summary>
     /// <remarks>
     /// <B>Windows Server 2008, Windows Vista, Windows Server 2003, and Windows XP:</B>  This value is not used.
     /// </remarks>
     WTSOutgoingFrames,

     /// <summary>
     /// Information about a Remote Desktop Connection (RDC) client. For more information, see <see cref="WTSCLIENT"/>.
     /// </summary>
     /// <remarks>
     /// <B>Windows Vista, Windows Server 2003, and Windows XP:</B>  This value is not supported. 
     /// This value is supported beginning with Windows Server 2008 and Windows Vista with SP1.
     /// </remarks>
     WTSClientInfo,

     /// <summary>
     /// Information about a client session on an RD Session Host server. For more information, see <see cref="WTSINFO"/>.
     /// </summary>
     /// <remarks>
     /// <B>Windows Vista, Windows Server 2003, and Windows XP:</B>  This value is not supported. 
     /// This value is supported beginning with Windows Server 2008 and Windows Vista with SP1.
     /// </remarks>
     WTSSessionInfo
}
```

## VB Definition:
```cs
Private Enum WTS_INFO_CLASS
    WTSInitialProgram
    WTSApplicationName
    WTSWorkingDirectory
    WTSOEMId
    WTSSessionId
    WTSUserName
    WTSWinStationName
    WTSDomainName
    WTSConnectState
    WTSClientBuildNumber
    WTSClientName
    WTSClientDirectory
    WTSClientProductId
    WTSClientHardwareId
    WTSClientAddress
    WTSClientDisplay
    WTSClientProtocolType
    WTSIdleTime
    WTSLogonTime
    WTSIncomingBytes
    WTSOutgoingBytes
    WTSIncomingFrames
    WTSOutgoingFrames
    WTSClientInfo
    WTSSessionInfo
    End Enum
```
