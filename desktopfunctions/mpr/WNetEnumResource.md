
## C# Signature:
```cs
[DllImport("mpr.dll")]
public static extern uint WNetEnumResource(IntPtr hEnum, ref int lpcCount, IntPtr lpBuffer, ref uint lpBufferSize);
```

## VB.NET Signature:
```cs
<DllImport("mpr.dll")> _
Public Shared Function WNetEnumResource(hEnum As IntPtr, ByRef lpcCount As Integer, lpBuffer As IntPtr, ByRef lpBufferSize As UInteger) As UInteger
End Function
```

## C# Sample Code:
```cs
// Coded by Eugene E. Zhukovsky, 8.21.2002
// Added by Kill
// declare the DLL import functions 

[DllImport("mpr.dll", CharSet=CharSet.Auto)]
  public static extern int WNetEnumResource(
    IntPtr hEnum, 
    ref int lpcCount,
    IntPtr lpBuffer, 
    ref int lpBufferSize );

[DllImport("mpr.dll", CharSet=CharSet.Auto)]
  public static extern int WNetOpenEnum(
    RESOURCE_SCOPE dwScope, 
    RESOURCE_TYPE dwType,
    RESOURCE_USAGE dwUsage, 
    [MarshalAs(UnmanagedType.AsAny)][In] Object lpNetResource, 
    out IntPtr lphEnum);

[DllImport("mpr.dll", CharSet=CharSet.Auto)]
  public static extern int WNetCloseEnum( IntPtr hEnum );
//declare the structures to hold info

public enum RESOURCE_SCOPE
{
    RESOURCE_CONNECTED = 0x00000001,
    RESOURCE_GLOBALNET = 0x00000002,
    RESOURCE_REMEMBERED = 0x00000003,
    RESOURCE_RECENT= 0x00000004,
    RESOURCE_CONTEXT= 0x00000005
}

public enum RESOURCE_TYPE
{
    RESOURCETYPE_ANY= 0x00000000,
    RESOURCETYPE_DISK= 0x00000001,
    RESOURCETYPE_PRINT = 0x00000002,
    RESOURCETYPE_RESERVED = 0x00000008,
}

public enum RESOURCE_USAGE
{
    RESOURCEUSAGE_CONNECTABLE =0x00000001,
    RESOURCEUSAGE_CONTAINER=0x00000002,
    RESOURCEUSAGE_NOLOCALDEVICE =0x00000004,
    RESOURCEUSAGE_SIBLING=0x00000008,
    RESOURCEUSAGE_ATTACHED=0x00000010,
    RESOURCEUSAGE_ALL =(RESOURCEUSAGE_CONNECTABLE | RESOURCEUSAGE_CONTAINER | RESOURCEUSAGE_ATTACHED),
}

public enum RESOURCE_DISPLAYTYPE
{
    RESOURCEDISPLAYTYPE_GENERIC= 0x00000000,
    RESOURCEDISPLAYTYPE_DOMAIN= 0x00000001,
    RESOURCEDISPLAYTYPE_SERVER= 0x00000002,
    RESOURCEDISPLAYTYPE_SHARE= 0x00000003,
    RESOURCEDISPLAYTYPE_FILE = 0x00000004,
    RESOURCEDISPLAYTYPE_GROUP= 0x00000005,
    RESOURCEDISPLAYTYPE_NETWORK= 0x00000006,
    RESOURCEDISPLAYTYPE_ROOT = 0x00000007,
    RESOURCEDISPLAYTYPE_SHAREADMIN = 0x00000008,
    RESOURCEDISPLAYTYPE_DIRECTORY = 0x00000009,
    RESOURCEDISPLAYTYPE_TREE = 0x0000000A,
    RESOURCEDISPLAYTYPE_NDSCONTAINER = 0x0000000B
}

public struct NETRESOURCE
{
    public RESOURCE_SCOPE dwScope;
    public RESOURCE_TYPE dwType;
    public RESOURCE_DISPLAYTYPE dwDisplayType;
    public RESOURCE_USAGE dwUsage;
    [MarshalAs(System.Runtime.InteropServices.UnmanagedType.LPTStr)] public string lpLocalName;
    [MarshalAs(System.Runtime.InteropServices.UnmanagedType.LPTStr)] public string lpRemoteName;
    [MarshalAs(System.Runtime.InteropServices.UnmanagedType.LPTStr)] public string lpComment;
    [MarshalAs(System.Runtime.InteropServices.UnmanagedType.LPTStr)] public string lpProvider;
}

//the function we'll be calling 

public static void WNETOE(Object o)
{
    int iRet;
    IntPtr ptrHandle = new IntPtr();
    try
    {
       iRet =WNetOpenEnum( 
       RESOURCE_SCOPE.RESOURCE_GLOBALNET, 
       RESOURCE_TYPE.RESOURCETYPE_ANY,
       RESOURCE_USAGE.RESOURCEUSAGE_ALL, 
       o, 
       out ptrHandle );
       if( iRet != 0 )
       { 
     return; 
       }

       int entries;
       int buffer = 16384;
       IntPtr ptrBuffer = Marshal.AllocHGlobal( buffer );
       NETRESOURCE nr;
       for(;;)
       {
      entries = -1;
      buffer = 16384;
     iRet =WNetEnumResource( ptrHandle, ref entries, ptrBuffer, ref buffer );
     if( (iRet != 0) || (entries < 1) )
     {
        break;
     }
     IntPtr ptr = ptrBuffer;
     for( int i = 0; i < entries; i++ )
     {
        nr = (NETRESOURCE)Marshal.PtrToStructure( ptr, typeof(NETRESOURCE) );
        if(RESOURCE_USAGE.RESOURCEUSAGE_CONTAINER == (nr.dwUsage
            & RESOURCE_USAGE.RESOURCEUSAGE_CONTAINER))
        {
         //call recursively to get all entries in a container
         WNETOE(nr);
        }
        ptr += Marshal.SizeOf( nr );
        Console.WriteLine( " {0} : LocalName='{1}' RemoteName='{2}'",
        nr.dwDisplayType.ToString(), nr.lpLocalName, nr.lpRemoteName );
     }
       }
       Marshal.FreeHGlobal( ptrBuffer );
       iRet =WNetCloseEnum( ptrHandle );
    }
    catch(Exception e)
    {
    }
}

//now call the function passing a null
WNETOE(null);

//here's some possible error codes
public enum NERR
{
    NERR_Success = 0,/* Success */
    ERROR_MORE_DATA = 234, // dderror
    ERROR_NO_BROWSER_SERVERS_FOUND = 6118,
    ERROR_INVALID_LEVEL = 124,
    ERROR_ACCESS_DENIED = 5,
    ERROR_INVALID_PARAMETER = 87,
    ERROR_NOT_ENOUGH_MEMORY = 8,
    ERROR_NETWORK_BUSY = 54,
    ERROR_BAD_NETPATH = 53,
    ERROR_NO_NETWORK = 1222,
    ERROR_INVALID_HANDLE_STATE = 1609,
    ERROR_EXTENDED_ERROR= 1208
}
```

## VB.Net Sample Code
```cs
' Added by Pete Doxtader on 06/05/2012
' This is a VB.NET port of the C# code above, 
' mostly done by Dan Halford on 2011/08/30.
' Added: GetNetworkDrives and GetNetworkComputers,
' and all functions now return a list(Of String).

Imports System.Runtime.InteropServices

Module modEnumResource

#Region "Enumnerations"

    Public Enum RESOURCE_SCOPE
    RESOURCE_CONNECTED = &H1
    RESOURCE_GLOBALNET = &H2
    RESOURCE_REMEMBERED = &H3
    RESOURCE_RECENT = &H4
    RESOURCE_CONTEXT = &H5
    End Enum

    Public Enum RESOURCE_TYPE
    RESOURCETYPE_ANY = &H0
    RESOURCETYPE_DISK = &H1
    RESOURCETYPE_PRINT = &H2
    RESOURCETYPE_RESERVED = &H8
    End Enum

    Public Enum RESOURCE_USAGE
    RESOURCEUSAGE_CONNECTABLE = &H1
    RESOURCEUSAGE_CONTAINER = &H2
    RESOURCEUSAGE_NOLOCALDEVICE = &H4
    RESOURCEUSAGE_SIBLING = &H8
    RESOURCEUSAGE_ATTACHED = &H10
    RESOURCEUSAGE_ALL = (RESOURCEUSAGE_CONNECTABLE Or RESOURCEUSAGE_CONTAINER Or RESOURCEUSAGE_ATTACHED)
    End Enum

    Public Enum RESOURCE_DISPLAYTYPE
    RESOURCEDISPLAYTYPE_GENERIC = &H0
    RESOURCEDISPLAYTYPE_DOMAIN = &H1
    RESOURCEDISPLAYTYPE_SERVER = &H2
    RESOURCEDISPLAYTYPE_SHARE = &H3
    RESOURCEDISPLAYTYPE_FILE = &H4
    RESOURCEDISPLAYTYPE_GROUP = &H5
    RESOURCEDISPLAYTYPE_NETWORK = &H6
    RESOURCEDISPLAYTYPE_ROOT = &H7
    RESOURCEDISPLAYTYPE_SHAREADMIN = &H8
    RESOURCEDISPLAYTYPE_DIRECTORY = &H9
    RESOURCEDISPLAYTYPE_TREE = &HA
    RESOURCEDISPLAYTYPE_NDSCONTAINER = &HB
    End Enum

    Public Enum NERR
    NERR_Success = 0
    ERROR_MORE_DATA = 234
    ERROR_NO_BROWSER_SERVERS_FOUND = 6118
    ERROR_INVALID_LEVEL = 124
    ERROR_ACCESS_DENIED = 5
    ERROR_INVALID_PARAMETER = 87
    ERROR_NOT_ENOUGH_MEMORY = 8
    ERROR_NETWORK_BUSY = 54
    ERROR_BAD_NETPATH = 53
    ERROR_NO_NETWORK = 1222
    ERROR_INVALID_HANDLE_STATE = 1609
    ERROR_EXTENDED_ERROR = 1208
    End Enum

#End Region
#Region "Structures"

    Public Structure NETRESOURCE
    Public dwScope As RESOURCE_SCOPE
    Public dwType As RESOURCE_TYPE
    Public dwDisplayType As RESOURCE_DISPLAYTYPE
    Public dwUsage As RESOURCE_USAGE
    <MarshalAs(System.Runtime.InteropServices.UnmanagedType.LPTStr)> Public lpLocalName As String
    <MarshalAs(System.Runtime.InteropServices.UnmanagedType.LPTStr)> Public lpRemoteName As String
    <MarshalAs(System.Runtime.InteropServices.UnmanagedType.LPTStr)> Public lpComment As String
    <MarshalAs(System.Runtime.InteropServices.UnmanagedType.LPTStr)> Public lpProvider As String
    End Structure

#End Region

    <DllImport("mpr.dll", CharSet:=CharSet.Auto)> _
    Public Function WNetEnumResource(ByVal hEnum As IntPtr, ByRef lpcCount As Integer, ByVal lpBuffer As IntPtr, ByRef lpBufferSize As Integer) As Integer
    End Function

    <DllImport("mpr.dll", CharSet:=CharSet.Auto)> _
    Public Function WNetOpenEnum(ByVal dwScope As RESOURCE_SCOPE, ByVal dwType As RESOURCE_TYPE, ByVal dwUsage As RESOURCE_USAGE, ByRef lpNetResource As NETRESOURCE, ByRef lphEnum As IntPtr) As Integer
    End Function

    <DllImport("mpr.dll", CharSet:=CharSet.Auto)> _
    Public Function WNetCloseEnum(ByVal hEnum As IntPtr) As Integer
    End Function

    Public Function GetNetworkDrives(ByRef o As NETRESOURCE, ByRef networkDriveCollection As List(Of String)) As Boolean

    Dim iRet As Integer
    Dim ptrHandle As IntPtr = New IntPtr()

    Try
        iRet = WNetOpenEnum(RESOURCE_SCOPE.RESOURCE_REMEMBERED, RESOURCE_TYPE.RESOURCETYPE_ANY, RESOURCE_USAGE.RESOURCEUSAGE_ATTACHED, o, ptrHandle)
        If iRet <> 0 Then Exit Function

        Dim entries As Integer
        Dim buffer As Integer = 16384
        Dim ptrBuffer As IntPtr = Marshal.AllocHGlobal(buffer)
        Dim nr As NETRESOURCE

        Do
        entries = -1
        buffer = 16384
        iRet = WNetEnumResource(ptrHandle, entries, ptrBuffer, buffer)
        If iRet <> 0 Or entries < 1 Then Exit Do

        Dim ptr As IntPtr = ptrBuffer
        For count As Integer = 0 To entries - 1
            nr = CType(Marshal.PtrToStructure(ptr, GetType(NETRESOURCE)), NETRESOURCE)
            If (RESOURCE_USAGE.RESOURCEUSAGE_CONTAINER = (nr.dwUsage And RESOURCE_USAGE.RESOURCEUSAGE_CONTAINER)) Then
            If Not GetNetworkDrives(nr, networkDriveCollection) Then
                Throw New Exception("")
            End If
            End If

            ptr += Marshal.SizeOf(nr)
            networkDriveCollection.Add(String.Format(nr.lpLocalName & "=" & nr.lpRemoteName))
        Next
        Loop
        Marshal.FreeHGlobal(ptrBuffer)
        iRet = WNetCloseEnum(ptrHandle)
    Catch ex As Exception
        If ex.Message <> "" Then networkDriveCollection.Add(ex.Message)
        Return False
    End Try

    Return True
    End Function

    Public Function GetNetworkComputers(ByRef o As NETRESOURCE, ByRef networkComputersCollection As List(Of String)) As Boolean

    Dim iRet As Integer
    Dim ptrHandle As IntPtr = New IntPtr()

    Try
        iRet = WNetOpenEnum(RESOURCE_SCOPE.RESOURCE_GLOBALNET, RESOURCE_TYPE.RESOURCETYPE_ANY, RESOURCE_USAGE.RESOURCEUSAGE_CONTAINER, o, ptrHandle)
        If iRet <> 0 Then Exit Function

        Dim entries As Integer
        Dim buffer As Integer = 16384
        Dim ptrBuffer As IntPtr = Marshal.AllocHGlobal(buffer)
        Dim nr As NETRESOURCE

        Do
        entries = -1
        buffer = 16384
        iRet = WNetEnumResource(ptrHandle, entries, ptrBuffer, buffer)
        If iRet <> 0 Or entries < 1 Then Exit Do

        Dim ptr As Int32 = ptrBuffer.ToInt32
        For count As Integer = 0 To entries - 1
            nr = CType(Marshal.PtrToStructure(New IntPtr(ptr), GetType(NETRESOURCE)), NETRESOURCE)
            If (RESOURCE_USAGE.RESOURCEUSAGE_CONTAINER = (nr.dwUsage And RESOURCE_USAGE.RESOURCEUSAGE_CONTAINER)) Then
            If Not GetNetworkComputers(nr, networkComputersCollection) Then
                Throw New Exception("")
            End If
            End If

            ptr += Marshal.SizeOf(nr)
            If nr.lpRemoteName.Length > 2 Then
            If nr.lpRemoteName.Substring(0, 2) = "\\" Then
                networkComputersCollection.Add(String.Format(nr.lpRemoteName.Remove(0, 2)))
            End If
            End If

        Next
        Loop
        Marshal.FreeHGlobal(ptrBuffer)
        iRet = WNetCloseEnum(ptrHandle)
    Catch ex As Exception
        If ex.Message <> "" Then networkComputersCollection.Add(ex.Message)
        Return False
    End Try

    Return True
    End Function

    Public Function WNETOE(ByRef o As NETRESOURCE, ByRef resourceCollection As List(Of String)) As Boolean

    Dim iRet As Integer
    Dim ptrHandle As IntPtr = New IntPtr()

    Try
        iRet = WNetOpenEnum(RESOURCE_SCOPE.RESOURCE_GLOBALNET, RESOURCE_TYPE.RESOURCETYPE_ANY, RESOURCE_USAGE.RESOURCEUSAGE_CONTAINER, o, ptrHandle)
        If iRet <> 0 Then Exit Function

        Dim entries As Integer
        Dim buffer As Integer = 16384
        Dim ptrBuffer As IntPtr = Marshal.AllocHGlobal(buffer)
        Dim nr As NETRESOURCE

        Do
        entries = -1
        buffer = 16384
        iRet = WNetEnumResource(ptrHandle, entries, ptrBuffer, buffer)
        If iRet <> 0 Or entries < 1 Then Exit Do

        Dim ptr As Int32 = ptrBuffer.ToInt32
        For count As Integer = 0 To entries - 1
            nr = CType(Marshal.PtrToStructure(New IntPtr(ptr), GetType(NETRESOURCE)), NETRESOURCE)
            If (RESOURCE_USAGE.RESOURCEUSAGE_CONTAINER = (nr.dwUsage And RESOURCE_USAGE.RESOURCEUSAGE_CONTAINER)) Then
            If Not WNETOE(nr, resourceCollection) Then
                Throw New Exception("")
            End If
            End If

            ptr += Marshal.SizeOf(nr)
            resourceCollection.Add(String.Format(nr.lpLocalName & " = " & nr.lpRemoteName))
        Next
        Loop
        Marshal.FreeHGlobal(ptrBuffer)
        iRet = WNetCloseEnum(ptrHandle)
    Catch ex As Exception
        If ex.Message <> "" Then resourceCollection.Add(ex.Message)
        Return False
    End Try

    Return True
    End Function

End Module
```
