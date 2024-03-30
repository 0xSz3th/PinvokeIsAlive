
## C# Signature:
```cs
[DllImport("Netapi32.dll", CharSet=CharSet.Unicode)]
private static extern int NetShareEnum(
     StringBuilder ServerName,
     int level,
     ref IntPtr bufPtr,
     uint prefmaxlen,
     ref int entriesread,
     ref int totalentries,
     ref int resume_handle
     );
```

## VB Signature:
```cs
Declare Unicode Function NetShareEnum Lib "netapi32.dll" _
            (ByVal ServerName As StringBuilder, _
            ByVal level As Integer, _
            ByRef BufPtr As IntPtr, 
            ByVal prefmaxbufferlen As Integer, _
            ByRef entriesread As Integer, _
            ByRef totalentries As Integer, _
            ByRef resume_handle As Integer) As Integer
```

## VB Signature:
```cs
<DllImport("Netapi32.dll", CharSet:=CharSet.Auto, SetLastError:=True)> _
    Public Shared Function NetShareEnum( _
        ByVal ServerName As StringBuilder, _
        ByVal level As Integer, _
        ByRef BufPtr As IntPtr, _
        ByVal prefmaxbufferlen As Integer, _
        ByRef entriesread As Integer, _
        ByRef totalentries As Integer, _
        ByRef resume_handle As Integer) As Integer
    End Function
```

## User-Defined Types:
```cs
if you use C# Sample code; 
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Unicode)]
public struct SHARE_INFO_0
{
     public string shi0_netname;
}
const uint MAX_PREFERRED_LENGTH = 0xFFFFFFFF;
const int NERR_Success = 0;
```

## Notes:
```cs
[28-06-2007]
  VB Enumeration Function Added by JustAl
[2006-07-05]
VB Alternate Signature code added by KRONOS

[2004-06-11]
VB Def and Sample code added by RACKLEY

[2004-08-31]
C# Def and Sample code added by K.MORONO
```

## Sample Code:
```cs
''' <summary>
    ''' Enumerates the shares on Windows NT
    ''' </summary>
    ''' <param name="server">The server name</param>
    ''' <param name="shares">The ShareCollection</param>
    Protected Shared Sub EnumerateSharesNT(ByVal server As String, ByVal shares As ShareCollection)
        Dim level As Integer = 2
        Dim entriesRead As Integer, totalEntries As Integer, nRet As Integer, hResume As Integer = 0
        Dim pBuffer As IntPtr = IntPtr.Zero

        Try
        nRet = NetShareEnum(server, level, pBuffer, -1, entriesRead, totalEntries, _
         hResume)

        If ERROR_ACCESS_DENIED = nRet Then
            'Need admin for level 2, drop to level 1
            level = 1
            nRet = NetShareEnum(server, level, pBuffer, -1, entriesRead, totalEntries, _
             hResume)
        End If

        If NO_ERROR = nRet AndAlso entriesRead > 0 Then
            Dim t As Type = IIf((2 = level), GetType(SHARE_INFO_2), GetType(SHARE_INFO_1))
            Dim offset As Integer = Marshal.SizeOf(t)

            Dim i As Integer = 0, lpItem As Integer = pBuffer.ToInt32()
            While i < entriesRead
            Dim pItem As New IntPtr(lpItem)
            If 1 = level Then
                Dim si As SHARE_INFO_1 = DirectCast(Marshal.PtrToStructure(pItem, t), SHARE_INFO_1)
                shares.Add(si.NetName, "Access Denied", si.ShareType, si.Remark)
            Else
                Dim si As SHARE_INFO_2 = DirectCast(Marshal.PtrToStructure(pItem, t), SHARE_INFO_2)
                shares.Add(si.NetName, si.Path, si.ShareType, si.Remark)
            End If
            i += 1
            lpItem += offset
            End While

        End If
        Finally
        ' Clean up buffer allocated by system
        If IntPtr.Zero <> pBuffer Then
            NetApiBufferFree(pBuffer)
        End If
        End Try
    End Sub
```

## Sample Code:
```cs
Dim currentPtr As IntPtr
Dim BufPtr As IntPtr        'in
Dim dwEntriesread As Integer     'out
Dim dwTotalentries As Integer    'out
Dim dwResumehandle As Integer    'out
Dim nStructSize As Integer
Dim shi2 As SHARE_INFO_2
Dim cnt As Long         'share enumeration counter
Dim SvrNameBldr As New StringBuilder(ServerName)

retval = NetShareEnum(SvrNameBldr, 2, BufPtr, MAX_PREFERRED_LENGTH, dwEntriesread, dwTotalentries, dwResumehandle)

If retval = NERR_Success And retval <> ERROR_MORE_DATA Then
   currentPtr = BufPtr
   nStructSize = Marshal.SizeOf(GetType(SHARE_INFO_2))

   ' Enumerate over all shares on the server and find the any/all shares that point
   ' to c:\deletemeplease and delete those shares.
   For cnt = 0 To dwEntriesread - 1
     shi2 = Marshal.PtrToStructure(currentPtr, GetType(SHARE_INFO_2))
     If System.String.Compare(shi2.shi2_path, "c:\deletemeplease" True) = 0 Then
       DelRetVal = NetShareDel(ServerName, shi2.shi2_netname, 0)
     End If
     currentPtr = New IntPtr(currentPtr.ToInt32 + Marshal.SizeOf(GetType(SHARE_INFO_2)))
   Next

End If
Call NetApiBufferFree(BufPtr)

[C#]
PUT TextBox control,ListBox control and Button control on your Form.

private void button1_Click(object sender, System.EventArgs e)
{
     listBox1.Items.Clear();

     int entriesread = 0;
     int totalentries = 0;
     int resume_handle = 0;
     int nStructSize = Marshal.SizeOf(typeof(SHARE_INFO_0));
     IntPtr bufPtr = IntPtr.Zero;
     StringBuilder server = new StringBuilder(textBox1.Text);
     int ret = NetShareEnum(server,0,ref bufPtr,MAX_PREFERRED_LENGTH,ref entriesread,ref totalentries,ref resume_handle);
     if (ret == NERR_Success)
     {
     IntPtr currentPtr = bufPtr;
     for (int i = 0;i<entriesread;i++)
     {
         SHARE_INFO_0 shi0 = (SHARE_INFO_0)Marshal.PtrToStructure(currentPtr,typeof(SHARE_INFO_0));
         listBox1.Items.Add(shi0.shi0_netname);
         currentPtr += nStructSize;
     }
     NetApiBufferFree(bufPtr);
     } 
     else
     {
     listBox1.Items.Add("失敗 = " + ret.ToString());
     }
}
```

## Sample Class for SHARE_INFO_1 (sharename, sharetype, remark)
```cs
public class GetNetShares
{
    #region External Calls
    [DllImport("Netapi32.dll", SetLastError = true)]
    static extern int NetApiBufferFree(IntPtr Buffer);
    [DllImport("Netapi32.dll", CharSet = CharSet.Unicode)]
    private static extern int NetShareEnum(
         StringBuilder ServerName,
         int level,
         ref IntPtr bufPtr,
         uint prefmaxlen,
         ref int entriesread,
         ref int totalentries,
         ref int resume_handle
         );
    #endregion
    #region External Structures
    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
    public struct SHARE_INFO_1
    {
        public string shi1_netname;
        public uint shi1_type;
        public string shi1_remark;
        public SHARE_INFO_1(string sharename, uint sharetype, string remark)
        {
        this.shi1_netname = sharename;
        this.shi1_type = sharetype;
        this.shi1_remark = remark;
        }
        public override string ToString()
        {
        return shi1_netname;
        }
    }
    #endregion
    const uint MAX_PREFERRED_LENGTH = 0xFFFFFFFF;
    const int NERR_Success = 0;
    private enum NetError : uint
    {
        NERR_Success = 0,
        NERR_BASE = 2100,
        NERR_UnknownDevDir = (NERR_BASE + 16),
        NERR_DuplicateShare = (NERR_BASE + 18),
        NERR_BufTooSmall = (NERR_BASE + 23),
    }
    private enum SHARE_TYPE : uint
    {
        STYPE_DISKTREE = 0,
        STYPE_PRINTQ = 1,
        STYPE_DEVICE = 2,
        STYPE_IPC = 3,
        STYPE_SPECIAL = 0x80000000,
    }
    public SHARE_INFO_1[] EnumNetShares(string Server)
    {
        List<SHARE_INFO_1> ShareInfos = new List<SHARE_INFO_1>();
        int entriesread = 0;
        int totalentries = 0;
        int resume_handle = 0;
        int nStructSize = Marshal.SizeOf(typeof(SHARE_INFO_1));
        IntPtr bufPtr = IntPtr.Zero;
        StringBuilder server = new StringBuilder(Server);
        int ret = NetShareEnum(server, 1, ref bufPtr, MAX_PREFERRED_LENGTH, ref entriesread, ref totalentries, ref resume_handle);
        if (ret == NERR_Success)
        {
        IntPtr currentPtr = bufPtr;
        for (int i = 0; i < entriesread; i++)
        {
            SHARE_INFO_1 shi1 = (SHARE_INFO_1)Marshal.PtrToStructure(currentPtr, typeof(SHARE_INFO_1));
            ShareInfos.Add(shi1);
            currentPtr += nStructSize;
        }
        NetApiBufferFree(bufPtr);
        return ShareInfos.ToArray();
        }
        else
        {
        ShareInfos.Add(new SHARE_INFO_1("ERROR=" + ret.ToString(),10,string.Empty));
        return ShareInfos.ToArray();
        }
    }
}
```

## Sample Class for SHARE_INFO_1 (sharename, sharetype, remark)
```cs
'[VB.Net]
' What is mission. This one works well. Share type 0 is a normal shared folder. I don't know the other types
' but hey, the mission here is to list shares.
' Added by: Pieter E Jordaan - South Africa
'
' Usage :  ServerShareCollection = GetSharesFromHost("Server")
' For Each s As ShareType In ServerShareCollection.Shares
' msgbox (s.name)
' next
'

Imports System
Imports System.Runtime.InteropServices
Imports System.text

Module ShareModule
    Public ServerShareCollection As ShareCollection

    Public Structure ShareType
    Dim Name As String
    Dim Path As String
    Dim Type As Integer
    Dim Remark As String
    End Structure

    Public Structure ShareCollection
    Dim Shares() As ShareType
    Dim ShareCount As Integer

    Sub Clear()
        Shares = Nothing
    End Sub

    Sub Add(ByVal Name As String, ByVal Path As String, ByVal Type As Integer, ByVal Remark As String)
        If Shares Is Nothing Then
        ReDim Shares(0)
        Shares(0).Name = Name
        Shares(0).Path = Path
        Shares(0).Type = Type
        Shares(0).Remark = Remark
        Else
        ReDim Preserve Shares(Shares.Length)
        Shares(Shares.Length - 1).Name = Name
        Shares(Shares.Length - 1).Path = Path
        Shares(Shares.Length - 1).Type = Type
        Shares(Shares.Length - 1).Remark = Remark
        End If
        If Type = 0 Then ShareCount = ShareCount + 1
    End Sub
    End Structure

    Declare Unicode Function NetShareEnum Lib "netapi32.dll" _
        (ByVal ServerName As StringBuilder, _
        ByVal level As Integer, _
        ByRef BufPtr As IntPtr, _
        ByVal prefmaxbufferlen As Integer, _
        ByRef entriesread As Integer, _
        ByRef totalentries As Integer, _
        ByRef resume_handle As Integer) As Integer

    Declare Unicode Function NetShareGetInfo Lib "netapi32.dll" _
    (ByVal ServerName As String, _
    ByVal ShareName As String, _
    ByVal Level As Integer, _
    ByRef BufPtr As IntPtr) As Integer

    Declare Unicode Function NetApiBufferFree Lib "netapi32.dll" _
      (ByRef buffer As IntPtr) As Long



#Region "Constants"

    Const MAX_PREFERRED_LENGTH As Integer = -1      ' originally 0
    Const ERROR_SUCCESS As Long = 0&        ' No errors encountered.
    Const NERR_Success As Long = 0&
    Const ERROR_ACCESS_DENIED As Long = 5&      ' The user has insufficient privilege for this operation.
    Const ERROR_NOT_ENOUGH_MEMORY As Long = 8&      ' Not enough memory
    Const ERROR_NETWORK_ACCESS_DENIED As Long = 65&     ' Network access is denied.
    Const ERROR_INVALID_PARAMETER As Long = 87&     ' Invalid parameter specified.
    Const ERROR_BAD_NETPATH As Long = 53&       ' The network path was not found.
    Const ERROR_INVALID_NAME As Long = 123&     ' Invalid name
    Const ERROR_INVALID_LEVEL As Long = 124&    ' Invalid level parameter.
    Const ERROR_MORE_DATA As Long = 234&        ' More data available, buffer too small.
    Const NERR_BASE As Long = 2100&
    Const NERR_NetNotStarted As Long = 2102&    ' Device driver not installed.
    Const NERR_RemoteOnly As Long = 2106&       ' This operation can be performed only on a server.
    Const NERR_ServerNotStarted As Long = 2114&     ' Server service not installed.
    Const NERR_BufTooSmall As Long = 2123&      ' Buffer too small for fixed-length data.
    Const NERR_RemoteErr As Long = 2127&        ' Error encountered while remotely.  executing function
    Const NERR_WkstaNotStarted As Long = 2138&      ' The Workstation service is not started.
    Const NERR_BadTransactConfig As Long = 2141&    ' The server is not configured for this transaction;  IPC$ is not shared.
    Const NERR_NetNameNotFound As Long = (NERR_BASE + 210)  ' Sharename not found.
    Const NERR_InvalidComputer As Long = 2351&      ' Invalid computername specified.

#End Region ' "Constants"

#Region "API Calls With Structures"

    <StructLayout(LayoutKind.Sequential)> _
    Structure SHARE_INFO_1
    <MarshalAs(UnmanagedType.LPWStr)> Dim netname As String
    Public ShareType As Integer
    <MarshalAs(UnmanagedType.LPWStr)> Dim Remark As String

    End Structure

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

    Public Function GetSharesFromHost(ByVal server As String) As ShareCollection
    Dim Shares As New ShareCollection
    Shares.Clear()
    Dim level As Integer = 2
    Dim svr As New StringBuilder(server)
    Dim entriesRead As Integer, totalEntries As Integer, nRet As Integer, hResume As Integer = 0
    Dim pBuffer As IntPtr = IntPtr.Zero

    Try
        nRet = NetShareEnum(svr, level, pBuffer, -1, entriesRead, totalEntries, _
         hResume)

        If ERROR_ACCESS_DENIED = nRet Then
        'Need admin for level 2, drop to level 1
        level = 1
        nRet = NetShareEnum(svr, level, pBuffer, -1, entriesRead, totalEntries, _
         hResume)
        End If

        If 0 = nRet AndAlso entriesRead > 0 Then
        Dim t As Type = IIf((2 = level), GetType(SHARE_INFO_2), GetType(SHARE_INFO_1))
        Dim offset As Integer = Marshal.SizeOf(t)

        Dim i As Integer = 0, lpItem As Integer = pBuffer.ToInt32()
        While i < entriesRead
            Dim pItem As New IntPtr(lpItem)
            If 1 = level Then
            Dim si As SHARE_INFO_1 = DirectCast(Marshal.PtrToStructure(pItem, t), SHARE_INFO_1)
            Shares.Add(si.netname, "Access Denied", si.ShareType, si.Remark)
            Else
            Dim si As SHARE_INFO_2 = DirectCast(Marshal.PtrToStructure(pItem, t), SHARE_INFO_2)
            Shares.Add(si.shi2_netname, si.shi2_path, si.shi2_type, si.shi2_remark)
            End If
            i += 1
            lpItem += offset
        End While

        End If
        Return Shares
    Finally
        ' Clean up buffer allocated by system
        If IntPtr.Zero <> pBuffer Then
        NetApiBufferFree(pBuffer)
        End If

    End Try
    Return Shares
    End Function

End Module

' Enjoy!
```
