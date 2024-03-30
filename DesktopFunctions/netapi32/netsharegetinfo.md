
## C# Signature:
```cs
[DllImport("Netapi32.dll", SetLastError=true)]
public static extern int NetShareGetInfo(
    [MarshalAs(UnmanagedType.LPWStr)] string serverName,
    [MarshalAs(UnmanagedType.LPWStr)] string netName,
    Int32 level,
    out IntPtr bufPtr );
```

## VB Signature:
```cs
Declare Unicode Function NetShareGetInfo Lib "netapi32.dll" _
            (ByVal ServerName As String, _
            ByVal ShareName As String, _
            ByVal Level As Integer, _
            ByRef BufPtr As IntPtr) As Integer
```

## Notes:
```cs
[2004-06-11]
VB Def added by RACKLEY

[2004-09-03]
VB.NET Code added from Ralph Mallamace based on conversions from VB code on other sites

[2007-09-20]
Corrected VB Signature 'ByVal Level As Long' --> 'ByVal Level as Integer', format tidy.
```

## Sample Code:
```cs
Imports System
  Imports System.Runtime.InteropServices

  Module NetShareGetInfoAPI

  Declare Unicode Function NetShareGetInfo Lib "netapi32.dll" _
    (ByVal ServerName As String, _
    ByVal ShareName As String, _
    ByVal Level As Integer, _
    ByRef BufPtr As IntPtr) As Integer

  Declare Unicode Function NetApiBufferFree Lib "netapi32.dll" _
    (ByRef buffer As IntPtr) As Long
```

## Sample Code:
```cs
#Region "Constants"

    Const MAX_PREFERRED_LENGTH As Integer = -1          ' originally 0
    Const ERROR_SUCCESS As Long = 0&            ' No errors encountered.
    Const NERR_Success As Long = 0&
    Const ERROR_ACCESS_DENIED As Long = 5&          ' The user has insufficient privilege for this operation.
    Const ERROR_NOT_ENOUGH_MEMORY As Long = 8&          ' Not enough memory
    Const ERROR_NETWORK_ACCESS_DENIED As Long = 65&     ' Network access is denied.
    Const ERROR_INVALID_PARAMETER As Long = 87&         ' Invalid parameter specified.
    Const ERROR_BAD_NETPATH As Long = 53&           ' The network path was not found.
    Const ERROR_INVALID_NAME As Long = 123&         ' Invalid name
    Const ERROR_INVALID_LEVEL As Long = 124&        ' Invalid level parameter.
    Const ERROR_MORE_DATA As Long = 234&            ' More data available, buffer too small.
    Const NERR_BASE As Long = 2100&
    Const NERR_NetNotStarted As Long = 2102&        ' Device driver not installed.
    Const NERR_RemoteOnly As Long = 2106&           ' This operation can be performed only on a server.
    Const NERR_ServerNotStarted As Long = 2114&         ' Server service not installed.
    Const NERR_BufTooSmall As Long = 2123&          ' Buffer too small for fixed-length data.
    Const NERR_RemoteErr As Long = 2127&            ' Error encountered while remotely.  executing function
    Const NERR_WkstaNotStarted As Long = 2138&          ' The Workstation service is not started.
    Const NERR_BadTransactConfig As Long = 2141&        ' The server is not configured for this transaction;  IPC$ is not shared.
    Const NERR_NetNameNotFound As Long = (NERR_BASE + 210)  ' Sharename not found.
    Const NERR_InvalidComputer As Long = 2351&          ' Invalid computername specified.

  #End Region ' "Constants"

  #Region "API Calls With Structures"

    <StructLayout(LayoutKind.Sequential)> _
    Structure SHARE_INFO_2
        <MarshalAs(UnmanagedType.LPWStr)> Dim shi2_netname As String
        Dim shi2_type As Integer
        <MarshalAs(UnmanagedType.LPWStr)> Dim shi2_remark As String
        Dim shi2_permissions As Integer
        Dim shi2_max_uses As Integer
        Dim shi2_current_uses As Integer
        <MarshalAs(UnmanagedType.LPWStr)> Dim shi2_path As String
        <MarshalAs(UnmanagedType.LPWStr)> Dim shi2_passwd As String
    End Structure

  #End Region ' "API Calls With Structures"

  #Region "Methods"
    <MarshalAs(UnmanagedType.LPWStr)> Private sapiServer As String
    <MarshalAs(UnmanagedType.LPWStr)> Private sapiShare As String
    <MarshalAs(UnmanagedType.LPWStr)> Private sapiByteServer(1) As Char
    <MarshalAs(UnmanagedType.LPWStr)> Private sapiByteShare(1) As Char

    Public Function CallAPI_NetShareGetInfo(ByVal NetSharePath as String) As String
    'returns string of local file path for UNC share

        Dim Value as String        
        Dim sTemp as String
        Dim sServer as String
        Dim sShare As String
        Dim Result As Integer
        Dim pBuffer As New IntPtr(Marshal.SizeOf(GetType(SHARE_INFO_2)))
        Dim pCurrent As SHARE_INFO_2
        Dim sReturnBasePath as String

        ' Trim Beginning of NetSharePath into Value
        Value = NetSharePath.TrimStart

        '
        ' Set temp string to start of server name
        '
        If Value.Substring(0, 2) = "\\" Then
            sTemp = Value.Substring(2) 'Mid(Value, 3)
        Else
            sTemp = Value
        End If
        '
        ' Set Server name to the end of the first \
        '
        sServer = sTemp.Substring(0, sTemp.IndexOf("\"))
        '
        ' Error if Server not set
        '
        If sServer.Length = 0 Then
            ' Throw New Exception("FullPath  Error :- Server not specified")
        Else
            sapiServer = "\\" & sServer
        End If
        '
        ' Set Temp String to be at start of Share
        '
        sTemp = sTemp.Substring(sTemp.IndexOf("\") + 1)
        '
        ' Check if a slash is included at the beginning of the temp string
        '
        If sTemp.IndexOf("\") > 0 Then
            sShare = Left(sTemp, InStr(1, sTemp, "\") - 1)
            sTemp = Mid(sTemp, InStr(1, sTemp, "\"))
        Else
            sShare = sTemp
            sTemp = ""
        End If
        '
        ' Set Share to Upper Case
        '
        sapiShare = sShare.ToUpper
        '
        ' Do API Call
        '
        If sapiServer.Length > 0 Then
            '
            'Set up Server as marshalled char array with a null char at the end
            '
            ReDim sapiByteServer(sapiServer.Length)
            sapiServer.CopyTo(0, sapiByteServer, 0, sapiServer.Length)
            sapiByteServer(sapiServer.Length) = CChar(vbNullChar)
            '
            'Set up Share as marshalled char array with a null char at the end
            '
            ReDim sapiByteShare(sapiShare.Length)
            sapiShare.CopyTo(0, sapiByteShare, 0, sapiShare.Length)
            sapiByteShare(sapiShare.Length) = CChar(vbNullChar)
            '
            ' Call API
            '
            Result = Me.NetShareGetInfo(sapiByteServer, sapiByteShare, 2, pBuffer)
        Else
            '
            ' Call API and get network info on the share
            ' Note: By Sending Null were looking at current machine
            '
            Result = Me.NetShareGetInfo(vbEmpty, sapiByteShare, 2, pBuffer)
        End If

        '
        ' Read info from buffer if no errors
        '
        If Result = NERR_Success Then
            Dim currentPtr As IntPtr
            '
            ' Convert Buffer to SHARE_INFO_2
            '
            currentPtr = pBuffer
            pCurrent = CType(Marshal.PtrToStructure(currentPtr, GetType(SHARE_INFO_2)), SHARE_INFO_2)

            '
            ' Set Values from pCurrent
            '
            sReturnBasePath = pCurrent.shi2_path
        Else
            Select Case Result
            Case ERROR_ACCESS_DENIED
                Throw New Exception("NetShareGetInfo: ERROR_ACCESS_DENIED -> The user has insufficient privilege for this operation.")
            Case ERROR_NOT_ENOUGH_MEMORY
                Throw New Exception("NetShareGetInfo: ERROR_NOT_ENOUGH_MEMORY -> Not enough memory")
            Case ERROR_NETWORK_ACCESS_DENIED
                Throw New Exception("NetShareGetInfo: ERROR_NETWORK_ACCESS_DENIED -> Network access is denied.")
            Case ERROR_INVALID_PARAMETER
                Throw New Exception("NetShareGetInfo: ERROR_INVALID_PARAMETER Invalid parameter specified.")
            Case ERROR_BAD_NETPATH
                Throw New Exception("NetShareGetInfo: ERROR_BAD_NETPATH -> The network path was not found.")
            Case ERROR_INVALID_NAME
                Throw New Exception("NetShareGetInfo: ERROR_INVALID_NAME -> Invalid name")
            Case ERROR_INVALID_LEVEL
                Throw New Exception("NetShareGetInfo: ERROR_INVALID_LEVEL -> Invalid level parameter.")
            Case ERROR_MORE_DATA
                Throw New Exception("NetShareGetInfo: ERROR_MORE_DATA -> More data available, buffer too small.")
            Case NERR_NetNotStarted
                Throw New Exception("NetShareGetInfo: NERR_NetNotStarted -> Device driver not installed.")
            Case NERR_RemoteOnly
                Throw New Exception("NetShareGetInfo: NERR_RemoteOnly -> This operation can be performed only on a server.")
            Case NERR_ServerNotStarted
                Throw New Exception("NetShareGetInfo: NERR_ServerNotStarted -> Server service not installed.")
            Case NERR_BufTooSmall
                Throw New Exception("NetShareGetInfo: NERR_BufTooSmall -> Buffer too small for fixed-length data.")
            Case NERR_RemoteErr
                Throw New Exception("NetShareGetInfo: NERR_RemoteErr -> Error encountered while remotely executing function")
            Case NERR_WkstaNotStarted
                Throw New Exception("NetShareGetInfo: NERR_WkstaNotStarted -> The Workstation service is not started.")
            Case NERR_BadTransactConfig
                Throw New Exception("NetShareGetInfo: NERR_BadTransactConfig -> The server is not configured for this transaction;  IPC$ is not shared.")
            Case NERR_NetNameNotFound
                Throw New Exception("NetShareGetInfo: NERR_NetNameNotFound -> Sharename not found.")
            Case NERR_InvalidComputer
                Throw New Exception("NetShareGetInfo: NERR_InvalidComputer -> Invalid computername specified.")
            Case Else
                Throw New Exception("NetShareGetInfo: Unknown " & Result)
            End Select
        End If
        '
        ' Free up buffer
        '
        Result = CInt(NetApiBufferFree(pBuffer))

        Return sReturnBasePath
    End Function

  #End Region ' "Methods"
```

## Sample Code:
```cs
public static extern int NetShareGetInfo(
            [MarshalAs(UnmanagedType.LPWStr)] string serverName,
            [MarshalAs(UnmanagedType.LPWStr)] string netName,
            Int32 level,
            out IntPtr bufPtr );
```

## Sample Code:
```cs
[ StructLayout( LayoutKind.Sequential )]
            public struct SHARE_INFO_502
        {
            [MarshalAs(UnmanagedType.LPWStr)]
            public string shi502_netname;
            public uint shi502_type;
            [MarshalAs(UnmanagedType.LPWStr)]
            public string shi502_remark;
            public Int32 shi502_permissions;
            public Int32 shi502_max_uses;
            public Int32 shi502_current_uses;
            [MarshalAs(UnmanagedType.LPWStr)]
            public string shi502_path;
            public IntPtr shi502_passwd;
            public Int32 shi502_reserved;
            public IntPtr shi502_security_descriptor;
        }
```

## Sample Code:
```cs
Result  = 0&             ' No errors encountered.
     Result  = 0&    
     Result  = 5&             ' The user has insufficient privilege for this operation.
     Result  = 8&             ' Not enough memory
     Result  = 65&            ' Network access is denied.
     Result = 87&             ' Invalid parameter specified.
     Result  = 53&            ' The network path was not found.
     Result  = 123&               ' Invalid name
     Result  = 124&               ' Invalid level parameter.
     Result = 234&            ' More data available, buffer too small.
     Result = 2100&
     Result  = 2102&               '   Device driver not installed.
     Result  = 2106&                 '   This operation can be performed only on a server.
     Result = 2114&               '   Server service not installed.
     Result = 2123&                 '   Buffer too small for fixed-length data.
     Result = 2127&                '   Error encountered while remotely.  executing function
     Result = 2138&              '  The Workstation service is not started.
     Result = 2141&              '   The server is not configured for this transaction;  IPC$ is not shared.
     Result = 2310&              '  Sharename not found.
     Result = (Result  + 210)          '   Sharename not found.
     Result = 2351&              '   Invalid computername specified.
```

## The following is a C# example; much the same as above. For questions comments feel free to mail mailto:wshore@dstoutput.ca
```cs
using System;
    using System.Collections;
    using System.IO;
    using System.Runtime.InteropServices;
    using System.Text;
```

## The following is a C# example; much the same as above. For questions comments feel free to mail mailto:wshore@dstoutput.ca
```cs
class MainConsole
    {
         [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto)]
        struct SHARE_INFO_2
        {
            [MarshalAs(UnmanagedType.LPWStr)]
            public string shi2_netname;
            public uint shi2_type;
            [MarshalAs(UnmanagedType.LPWStr)]
            public string shi2_remark;
            public uint shi2_permissions;
            public uint shi2_max_uses;
            public uint shi2_current_uses;
            [MarshalAs(UnmanagedType.LPWStr)]
            public string shi2_path;
            [MarshalAs(UnmanagedType.LPWStr)]
            public string shi2_passwd;
        }

        static string FormatMessage(int errCode)
        {
            switch (errCode)
            {
                case ERROR_ACCESS_DENIED: return "The user does not have access to the requested information.";
                case ERROR_INVALID_LEVEL: return "The value specified for the level parameter is invalid.";
                case ERROR_INVALID_PARAMETER: return "The specified parameter is invalid.";
                case ERROR_MORE_DATA: return "More entries are available. Specify a large enough buffer to receive all entries.";
                case ERROR_NOT_ENOUGH_MEMORY: return "Insufficient memory is available.";
                case NERR_BufTooSmall: return "The supplied buffer is too small.";
                case NERR_NetNameNotFound: return "The share name does not exist.";
            };

            return null;
        }

        [DllImport("Netapi32", CharSet=CharSet.Auto)]
        static extern int NetApiBufferFree(IntPtr Buffer);

        [DllImport("Netapi32", CharSet=CharSet.Auto)]
        static extern int NetShareGetInfo([MarshalAs(UnmanagedType.LPWStr)] string servername,
            [MarshalAs(UnmanagedType.LPWStr)] string netname, int level, ref IntPtr bufptr);

        /// <summary>
        /// Retrieves the local path for the given server and share name.
        /// </summary>
        /// <remarks>serverName must start with \\</remarks>
        static string NetShareGetPath(string serverName, string netName)
        {
            string path = null;
            IntPtr ptr = IntPtr.Zero;

            int errCode = NetShareGetInfo(serverName, netName, 2, ref ptr);
            if (errCode == NERR_Success)
            {
                SHARE_INFO_2 shareInfo = (SHARE_INFO_2)
                    Marshal.PtrToStructure(ptr, typeof(SHARE_INFO_2));

                path = shareInfo.shi2_path;
                NetApiBufferFree(ptr);
            }
            else
                Console.WriteLine(FormatMessage(errCode));

            return path;
        }

        /// <summary>
        /// The Main method is the entry point of the program, where the program control starts and
        /// ends.
        /// </summary>
        /// <param name="args"></param>
        /// <returns></returns>
        [STAThread]
        static int Main(string [] args)
        {
            Console.WriteLine("path=" + NetShareGetPath("\\\\remote_server", "share_name"));

            return 0;
        }

        const int ERROR_ACCESS_DENIED = 5;
        const int ERROR_INVALID_LEVEL = 124; // unimplemented level for info
        const int ERROR_INVALID_PARAMETER = 87;
        const int ERROR_MORE_DATA = 234;
        const int ERROR_NOT_ENOUGH_MEMORY = 8;
        const int NERR_BufTooSmall = 2123; // The API return buffer is too small.
        const int NERR_NetNameNotFound = 2310; // This shared resource does not exist.
        const int NERR_Success = 0;

    } // class MainConsole
```

## Alternative Managed API:
```cs
http://social.msdn.microsoft.com/Forums/en-US/vblanguage/thread/b670a57f-8cc7-4f68-ab78-e47caa9d521b/
```

## Alternative Managed API:
```cs
Imports System.Management

    Module Main

    Sub Main()
        Dim Response As Integer
        Dim strShareName, strSharePath As String
        Dim oManager As ManagementClass
        Dim oShare As ManagementObject

        oManager = New ManagementClass("Win32_Share")
        For Each oShare In oManager.GetInstances()
            strShareName = oShare.Properties("Name").Value
            strSharePath = oShare.Properties("Path").Value
            If strSharePath = "" Then
                strSharePath = "***UNDEFINED***"
            End If
            Console.WriteLine(strShareName & " - " & strSharePath)
        Next

        Console.WriteLine("Hit <ENTER> to close window...")
        Response = Console.Read() ' Wait before closing
    End Sub ' Main

    End Module ' Main
```
