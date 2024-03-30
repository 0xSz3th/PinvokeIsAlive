
## C# Signature:
```cs
[DllImport("netapi32.dll", SetLastError=true)]
        private static extern int NetSessionEnum(
            [In,MarshalAs(UnmanagedType.LPWStr)] string ServerName,
            [In,MarshalAs(UnmanagedType.LPWStr)] string UncClientName,
            [In,MarshalAs(UnmanagedType.LPWStr)] string UserName,
            Int32 Level,
            out IntPtr bufptr,
            int prefmaxlen,
            ref Int32 entriesread,
            ref Int32 totalentries,
            ref Int32 resume_handle);
```

## VB Signature:
```cs
''' <summary>
    ''' The NetSessionEnum function provides information about sessions established on a server.
    ''' </summary>
    ''' <param name="serverName">[in] Pointer to a string that specifies the DNS or NetBIOS name of the remote server on which the function is to execute. If this parameter is NULL, the local computer is used.</param>
    ''' <param name="UncClientName">[in] Pointer to a string that specifies the name of the computer session for which information is to be returned. If this parameter is NULL, NetSessionEnum returns information for all computer sessions on the server.</param>
    ''' <param name="userName">[in] Pointer to a string that specifies the name of the user for which information is to be returned. If this parameter is NULL, NetSessionEnum returns information for all users.</param>
    ''' <param name="level">[in] Specifies the information level of the data. This parameter can be one of the following values.
    ''' <list>
    ''' <listheader></listheader>
    ''' <item>0 - Return the name of the computer that established the session. The bufptr parameter points to an array of SESSION_INFO_0 structures. </item>
    ''' <item>1 - Return the name of the computer, name of the user, and open files, pipes, and devices on the computer. The bufptr parameter points to an array of SESSION_INFO_1 structures. </item>
    ''' <item>2 - In addition to the information indicated for level 1, return the type of client and how the user established the session. The bufptr parameter points to an array of SESSION_INFO_2 structures. </item>
    ''' <item>10 - Return the name of the computer, name of the user, and active and idle times for the session. The bufptr parameter points to an array of SESSION_INFO_10 structures. </item>
    ''' <item>502 - Return the name of the computer; name of the user; open files, pipes, and devices on the computer; and the name of the transport the client is using. The bufptr parameter points to an array of SESSION_INFO_502 structures. </item>
    ''' </list>
    ''' </param>
    ''' <param name="bufptr">
    ''' [out] Pointer to the buffer that receives the data. The format of this data depends on the value of the level parameter. 
    ''' This buffer is allocated by the system and must be freed using the NetApiBufferFree function. Note that you must free the buffer even if the function fails with ERROR_MORE_DATA.
    ''' </param>
    ''' <param name="prefmaxlen">[in] Specifies the preferred maximum length of returned data, in bytes. If you specify MAX_PREFERRED_LENGTH, the function allocates the amount of memory required for the data. If you specify another value in this parameter, it can restrict the number of bytes that the function returns. If the buffer size is insufficient to hold all entries, the function returns ERROR_MORE_DATA.</param>
    ''' <param name="entriesread">[out] Pointer to a value that receives the count of elements actually enumerated.</param>
    ''' <param name="totalentries">[out] Pointer to a value that receives the total number of entries that could have been enumerated from the current resume position. Note that applications should consider this value only as a hint.</param>
    ''' <param name="resume_handle">[in, out] Pointer to a value that contains a resume handle which is used to continue an existing session search. The handle should be zero on the first call and left unchanged for subsequent calls. If resume_handle is NULL, no resume handle is stored.</param>
    ''' <returns>If the function succeeds, the return value is NERR_Success.
    ''' If the function fails, the return value can be one of the following error codes.
    ''' <list>
    ''' <item>ERROR_ACCESS_DENIED - The user does not have access to the requested information.</item>
    ''' <item>ERROR_INVALID_LEVEL - The value specified for the level parameter is invalid. </item>
    ''' <item>ERROR_INVALID_PARAMETER - The specified parameter is invalid. </item>
    ''' <item>ERROR_MORE_DATA - More entries are available. Specify a large enough buffer to receive all entries. </item>
    ''' <item>ERROR_NOT_ENOUGH_MEMORY - Insufficient memory is available. </item>
    ''' <item>NERR_ClientNameNotFound - A session does not exist with the computer name. </item>
    ''' <item>NERR_InvalidComputer - The computer name is invalid. </item>
    ''' <item>NERR_UserNotFound - The user name could not be found. </item>
    ''' </list>
    ''' </returns>
    ''' <remarks></remarks>
    <DllImport("netapi32.dll", SetLastError:=True)> _
    Private Shared Function NetSessionEnum( _
        <MarshalAs(UnmanagedType.LPWStr)> ByVal serverName As String, _
        <MarshalAs(UnmanagedType.LPWStr)> ByVal UncClientName As String, _
        <MarshalAs(UnmanagedType.LPWStr)> ByVal userName As String, _
        ByVal level As Integer, _
        ByRef bufptr As IntPtr, _
        ByVal prefmaxlen As Integer, _
        ByRef entriesread As Integer, _
        ByRef totalentries As Integer, _
        ByRef resume_handle As Integer) As Integer

    End Function
```

## C# Signature:
```cs
[ StructLayout( LayoutKind.Sequential )]public struct SESSION_INFO_502
    {
        /// <summary>
        /// Unicode string specifying the name of the computer that established the session.
        /// </summary>
        [MarshalAs(UnmanagedType.LPWStr)]public string sesi502_cname;
        /// <summary>
        /// <value>Unicode string specifying the name of the user who established the session.</value>
        /// </summary>
        [MarshalAs(UnmanagedType.LPWStr)]public string sesi502_username;
        /// <summary>
        /// <value>Specifies the number of files, devices, and pipes opened during the session.</value>
        /// </summary>
        public uint sesi502_num_opens;
        /// <summary>
        /// <value>Specifies the number of seconds the session has been active. </value>
        /// </summary>
        public uint sesi502_time;
        /// <summary>
        /// <value>Specifies the number of seconds the session has been idle.</value>
        /// </summary>
        public uint sesi502_idle_time;
        /// <summary>
        /// <value>Specifies a value that describes how the user established the session.</value>
        /// </summary>
        public uint sesi502_user_flags;
        /// <summary>
        /// <value>Unicode string that specifies the type of client that established the session.</value>
        /// </summary>
        [MarshalAs(UnmanagedType.LPWStr)]public string sesi502_cltype_name;
        /// <summary>
        /// <value>Specifies the name of the transport that the client is using to communicate with the server.</value>
        /// </summary>
        [MarshalAs(UnmanagedType.LPWStr)]public string sesi502_transport;
    }
```

## C# Signature:
```cs
public enum NERR
    {
        /// <summary>
        /// Operation was a success.
        /// </summary>
        NERR_Success = 0,
        /// <summary>
        /// More data available to read. dderror getting all data.
        /// </summary>
        ERROR_MORE_DATA = 234,
        /// <summary>
        /// Network browsers not available.
        /// </summary>
        ERROR_NO_BROWSER_SERVERS_FOUND = 6118,
        /// <summary>
        /// LEVEL specified is not valid for this call.
        /// </summary>
        ERROR_INVALID_LEVEL = 124,
        /// <summary>
        /// Security context does not have permission to make this call.
        /// </summary>
        ERROR_ACCESS_DENIED = 5,
        /// <summary>
        /// Parameter was incorrect.
        /// </summary>
        ERROR_INVALID_PARAMETER = 87,
        /// <summary>
        /// Out of memory.
        /// </summary>
        ERROR_NOT_ENOUGH_MEMORY = 8,
        /// <summary>
        /// Unable to contact resource. Connection timed out.
        /// </summary>
        ERROR_NETWORK_BUSY = 54,
        /// <summary>
        /// Network Path not found.
        /// </summary>
        ERROR_BAD_NETPATH = 53,
        /// <summary>
        /// No available network connection to make call.
        /// </summary>
        ERROR_NO_NETWORK = 1222,
        /// <summary>
        /// Pointer is not valid.
        /// </summary>
        ERROR_INVALID_HANDLE_STATE = 1609,
        /// <summary>
        /// Extended Error.
        /// </summary>
        ERROR_EXTENDED_ERROR= 1208,
        /// <summary>
        /// Base.
        /// </summary>
        NERR_BASE = 2100,
        /// <summary>
        /// Unknown Directory.
        /// </summary>
        NERR_UnknownDevDir = (NERR_BASE + 16),
        /// <summary>
        /// Duplicate Share already exists on server.
        /// </summary>
        NERR_DuplicateShare = (NERR_BASE + 18),
        /// <summary>
        /// Memory allocation was to small.
        /// </summary>
        NERR_BufTooSmall = (NERR_BASE + 23)
    }
```

## VB Signature:
```cs
<StructLayout(LayoutKind.Sequential)> Public Structure SESSION_INFO_502
    ' <summary>
    ' Unicode string specifying the name of the computer that established the session.
    ' </summary>
    <MarshalAs(UnmanagedType.LPTStr)> Public sesi502_cname As String
    ' <summary>
    ' <value>Unicode string specifying the name of the user who established the session.</value>
    ' </summary>
    <MarshalAs(UnmanagedType.LPTStr)> Public sesi502_username As String
    ' <summary>
    ' <value>Specifies the number of files, devices, and pipes opened during the session.</value>
    ' </summary>
    Public sesi502_num_opens As UInt32
    ' <summary>
    ' <value>Specifies the number of seconds the session has been active. </value>
    ' </summary>
    Public sesi502_time As UInt32
    ' <summary>
    ' <value>Specifies the number of seconds the session has been idle.</value>
    ' </summary>
    Public sesi502_idle_time As UInt32
    ' <summary>
    ' <value>Specifies a value that describes how the user established the session.</value>
    ' </summary>
    Public sesi502_user_flags As UInt32
    ' <summary>
    ' <value>Unicode string that specifies the type of client that established the session.</value>
    ' </summary>
    <MarshalAs(UnmanagedType.LPTStr)> Public sesi502_cltype_name As String
    ' <summary>
    ' <value>Specifies the name of the transport that the client is using to communicate with the server.</value>
    ' </summary>
    <MarshalAs(UnmanagedType.LPTStr)> Public sesi502_transport As String
    End Structure
```

## Sample Code: Vc
```cs
/// <summary>
        /// Returns all SESSIONS of the specified server. Returns an array of SESSION_INFO_502 structures.
        /// </summary>
        /// <param name="server">Server to get shares for without preceding backslashes.</param>
        /// <returns>SESSION_INFO_502 STRUCTURE ARRAY</returns>
        public static SESSION_INFO_502[] EnumSessions(string server)
        {
            IntPtr BufPtr;
            int res = 0;
            Int32 er=0,tr=0,resume=0;
            BufPtr = (IntPtr)Marshal.SizeOf(typeof(SESSION_INFO_502));
            SESSION_INFO_502[] results = new SESSION_INFO_502[0];
            do
            {
                res = NetSessionEnum(server,null,null,502,out BufPtr,-1,ref er,ref tr,ref resume);
                results = new SESSION_INFO_502[er];
                if (res == (int)NERR.ERROR_MORE_DATA || res == (int)NERR.NERR_Success)
                {
                    Int32 p = BufPtr.ToInt32();
                    for (int i = 0;i <er;i++)
                    {

                        SESSION_INFO_502 si = (SESSION_INFO_502)Marshal.PtrToStructure(new IntPtr(p),typeof(SESSION_INFO_502));
                        results[i] = si;
                        p += Marshal.SizeOf(typeof(SESSION_INFO_502));
                    }
                }
                Marshal.FreeHGlobal(BufPtr);
            }
            while (res==(int)NERR.ERROR_MORE_DATA); 
            return results;
        }
```

## Sample Code: VB
```cs
Public Shared Function SessionEnum(Optional ByVal sServer As String = "") As SESSION_INFO_502()
            Dim EntriesRead As Integer = 0
            Dim TotalRead As Integer = 0
            Dim ResumeHandle As Integer = 0
            Dim bufptr As IntPtr = 0
            Dim success As Integer
            Dim Result() As SESSION_INFO_502
            Dim i As Integer, ptr As IntPtr
            ReDim Result(0)
            If sServer = "" Then sServer = "\\" & Environ$("COMPUTERNAME")
            success = NetSessionEnum(sServer, "", "", 502, bufptr, -1, EntriesRead, TotalRead, ResumeHandle)
            If success = NERR.NERR_Success And success <> NERR.ERROR_MORE_DATA Then
                ReDim Result(EntriesRead - 1)
                For i = 0 To EntriesRead - 1
                ptr = bufptr.ToInt32 + (Marshal.SizeOf(Result(i)) * i)
                Result(i) = Marshal.PtrToStructure(ptr, Result(i).GetType)
                Next
            End If
            NetApiBufferFree(bufptr)
            Return Result
            End Function
```
