* Returns a valid handle to the FTP, Gopher, or HTTP session if the connection is successful, or NULL otherwise. To get extended error information, call GetLastError. An application can also use InternetGetLastResponseInfo to determine why access to the service was denied.

## C# Signature:
```cs
[DllImport("wininet.dll", SetLastError=true, CharSet=CharSet.Auto)]
static extern IntPtr InternetConnect(
   IntPtr hInternet, string lpszServerName, short nServerPort,
   string lpszUsername, string lpszPassword, int dwService,
   int dwFlags, IntPtr dwContext);
```

## VB Signature:
```cs
Declare Auto Function InternetConnect Lib "wininet.dll" (
    ByVal hInternetSession As System.IntPtr, 
    ByVal sServerName As String, 
    ByVal nServerPort As Integer, 
    ByVal sUsername As String, 
    ByVal sPassword As String, 
    ByVal lService As Int32, 
    ByVal lFlags As Int32,
    ByVal lContext As System.IntPtr) As System.IntPtr
```

## User-Defined Types:
```cs
Handle of the current Internet session. The handle must have been returned by a previous call to InternetOpen.
```

## User-Defined Types:
```cs
Address of a null-terminated string that contains the host name of an Internet server. Alternately, the string can contain the IP number of the site in ASCII dotted-decimal format (for example, 11.0.1.45).
```

## User-Defined Types:
```cs
Number of the TCP/IP port on the server to connect to. Can be one of the values in the following list. If this parameter is set to INTERNET_INVALID_PORT_NUMBER, the function uses the default port for the specified service. These values do not cause the function to use this protocol. The value sets the port to be used. A flag must be used to set the service.
    Value     Meaning
    INTERNET_DEFAULT_FTP_PORT     Use the default port for FTP servers (port 21).
    INTERNET_DEFAULT_GOPHER_PORT     Use the default port for Gopher servers (port 70).
    INTERNET_DEFAULT_HTTP_PORT     Use the default port for HTTP servers (port 80).
    INTERNET_DEFAULT_HTTPS_PORT     Use the default port for HTTPS servers (port 443).
```

## User-Defined Types:
```cs
Address of a null-terminated string that contains the name of the user to log on. If this parameter is NULL, the function uses an appropriate default, except for HTTP. A NULL parameter in HTTP causes the server to return an error. For the FTP protocol, the default is anonymous.
```

## User-Defined Types:
```cs
Address of a null-terminated string that contains the password to use to log on. If both lpszPassword and lpszUsername are NULL, the function uses the default anonymous password. In the case of FTP, the default anonymous password is the user's e-mail name. If lpszPassword is NULL, but lpszUsername is not NULL, the function uses a blank password. The following table describes the behavior for the four possible settings of lpszUsername and lpszPassword:
    lpszUsername     lpszPassword     User name sent to FTP server     Password sent to FTP server
    NULL     NULL     "anonymous"     User's e-mail name
    Non-NULL string     NULL     lpszUsername     ""
    NULL     Non-NULL string     ERROR     ERROR
    Non-NULL string     Non-NULL string     lpszUsername     lpszPassword
```

## User-Defined Types:
```cs
Type of service to access. Can be one of these values:
    Value     Meaning
    INTERNET_SERVICE_FTP     FTP service.
    INTERNET_SERVICE_GOPHER     Gopher service.
    INTERNET_SERVICE_HTTP     HTTP service.
```

## User-Defined Types:
```cs
Flags specific to the service used. Can be one of these values:
    If dwService is:     dwFlags supported
    INTERNET_SERVICE_FTP     INTERNET_CONNECT_FLAG_PASSIVE (Use passive mode in all data connections for this FTP session.)
```

## User-Defined Types:
```cs
An application-defined value that is used to identify the application context for the returned handle in callbacks.
```
