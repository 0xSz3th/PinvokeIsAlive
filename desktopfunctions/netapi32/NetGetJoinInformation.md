
## C# Signature:
```cs
[DllImport("Netapi32.dll", CharSet=CharSet.Unicode, SetLastError=true)]
static extern int NetGetJoinInformation(
  string server,
  out IntPtr domain,
  out NetJoinStatus status);
```

## VB Signature:
```cs
Private Declare Unicode Function NetGetJoinInformation Lib "Netapi32.dll" ( _
    ByVal lpServer As String, _
    ByRef lpNameBuffer As IntPtr, _
    ByRef bufferType As NETSETUP_JOIN_STATUS) _
    As NET_API_STATUS
```

## C# User-Defined Types:
```cs
// Win32 Result Code Constant
const int ErrorSuccess = 0;

// NetGetJoinInformation() Enumeration
public enum NetJoinStatus
{
    NetSetupUnknownStatus = 0,
    NetSetupUnjoined,
    NetSetupWorkgroupName,
    NetSetupDomainName
} // NETSETUP_JOIN_STATUS
```

## VB User-Defined Types and Enums:
```cs
Public Enum NETSETUP_JOIN_STATUS As UInteger
    NetSetupUnknownStatus = 0
    NetSetupUnjoined
    NetSetupWorkgroupName
    NetSetupDomainName
End Enum
```

## Alternative Managed API:
```cs
System.DirectoryServices.ActiveDirectory.Domain.GetComputerDomain();
```

## C# Sample Code:
```cs
[DllImport("Netapi32.dll")]
static extern int NetApiBufferFree(IntPtr Buffer);

// Returns the domain name the computer is joined to, or "" if not joined.
public static string GetJoinedDomain()
{
    int result = 0;
    string domain = null;
    IntPtr pDomain = IntPtr.Zero;
    NetJoinStatus status = NetJoinStatus.NetSetupUnknownStatus;
    try
    {
        result = NetGetJoinInformation(null, out pDomain, out status);
        if (result == ErrorSuccess &&
            status == NetJoinStatus.NetSetupDomainName)
        {
            domain = Marshal.PtrToStringAuto(pDomain);
        }
    }
    finally
    {
        if (pDomain != IntPtr.Zero) NetApiBufferFree(pDomain);
    }
    if (domain == null) domain = "";
    return domain;
}
```

## VB Sample Code
```cs
Imports System.Runtime.InteropServices

Public Structure NetGroupInformation
    Public GroupType As NETSETUP_JOIN_STATUS
    Public GroupName As String
End Structure

Public Enum NET_API_STATUS As UInteger
    NERR_Success = 0
    ERROR_NOT_ENOUGH_MEMORY = 8
End Enum

Public Enum NETSETUP_JOIN_STATUS As UInteger
    NetSetupUnknownStatus = 0
    NetSetupUnjoined
    NetSetupWorkgroupName
    NetSetupDomainName
End Enum

Public Class NetAPI
    Private Declare Unicode Function NetGetJoinInformation Lib "Netapi32.dll" ( _
        ByVal lpServer As String, _
        ByRef lpNameBuffer As IntPtr, _
        ByRef bufferType As NETSETUP_JOIN_STATUS) _
        As NET_API_STATUS

    Private Declare Function NetApiBufferFree Lib "Netapi32.dll" _
        (ByVal lpBuffer As IntPtr) As NET_API_STATUS

    Shared Function GetGroupInformation _
        (Optional ByVal ComputerName As String = vbNullString) As NetGroupInformation
        Dim status As NET_API_STATUS
        Dim bufPtr As IntPtr
        Dim groupInfo As NetGroupInformation = Nothing

        Try
            status = NetGetJoinInformation(ComputerName, bufPtr, groupInfo.GroupType)
            If status = NET_API_STATUS.NERR_Success Then 
                groupInfo.GroupName = Marshal.PtrToStringAuto(bufPtr)
            End If
        Finally
            If Not bufPtr = IntPtr.Zero Then NetApiBufferFree(bufPtr)
        End Try

        GetGroupInformation = groupInfo
    End Function
End Class
```
