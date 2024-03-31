
## C# Definition:
```cs
// The CharSet must match the CharSet of the corresponding PInvoke signature
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto)]
struct WIN32_FIND_DATA
{
    public uint dwFileAttributes;
    public System.Runtime.InteropServices.ComTypes.FILETIME ftCreationTime;
    public System.Runtime.InteropServices.ComTypes.FILETIME ftLastAccessTime;
    public System.Runtime.InteropServices.ComTypes.FILETIME ftLastWriteTime;
    public uint nFileSizeHigh;
    public uint nFileSizeLow;
    public uint dwReserved0;
    public uint dwReserved1;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst=260)]
    public string cFileName;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst=14)]
    public string cAlternateFileName;
    public uint dwFileType;
    public uint dwCreatorType;
    public uint wFinderFlags;
}
```

## VB.NET Definition:
```cs
' The CharSet must match the CharSet of the corresponding PInvoke signature
<StructLayout(LayoutKind.Sequential, CharSet := CharSet.Auto)> _
Structure WIN32_FIND_DATA
    Public dwFileAttributes As UInteger
    Public ftCreationTime As System.Runtime.InteropServices.ComTypes.FILETIME
    Public ftLastAccessTime As System.Runtime.InteropServices.ComTypes.FILETIME
    Public ftLastWriteTime As System.Runtime.InteropServices.ComTypes.FILETIME
    Public nFileSizeHigh As UInteger
    Public nFileSizeLow As UInteger
    Public dwReserved0 As UInteger
    Public dwReserved1 As UInteger
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst := 260)> Public cFileName As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst := 14)> Public cAlternateFileName As String
End Structure
```

## Notes:
```cs
/// <summary>
    /// Structure used for Windows API calls related to file information.
    /// </summary>
    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
    public struct WIN32_FIND_FILETIME
    {
    /// <summary>
    /// Specifies the low 32 bits of the FILETIME.
    /// </summary>
    public UInt32 dwLowDateTime;
    /// <summary>
    /// Specifies the high 32 bits of the FILETIME.
    /// </summary>
    public UInt32 dwHighDateTime;
    }
```

## VB.NET Definition:
```cs
'Use Pack:=4 to keep 8byte integers(Longs) from word alinging
  'yet allowing 4byte integers and the strings to properly align

  'requires: Imports System.Runtime.InteropServices

  <StructLayout(LayoutKind.Sequential, Pack:=4)> _
  Private Structure WIN32_FIND_DATA
    Public dwFileAttributes As Integer
    Public ftCreationTime As Long
    Public ftLastAccessTime As Long
    Public ftLastWriteTime As Long
    Public nFileSizeHigh As UInteger
    Public nFileSizeLow As UInteger
    Public dwReserved0 As Integer
    Public dwReserved1 As Integer
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=260)> Public cFileName As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=14)> Public cAlternate As String
  End Structure
```

## Notes:
```cs
Dim LastWrite As DateTime = DateTime.FromFileTime(ftLastWriteTime)
```

## Notes:
```cs
Dim FileSize As Long = ((nFileSizeHigh << 32&) Or nFileSizeLow)
```

## Notes:
```cs
Public dwLowDateTime As UInteger
    Public dwHighDateTime As UInteger
    Public Function ToDate() As Date
    Dim v = CLng(dwHighDateTime) << 32
    Return Date.FromFileTime(v + CLng(dwLowDateTime))
    End Function
```

## Notes:
```cs
<StructLayout(LayoutKind.Explicit, Pack:=4, Size:=8)> _
    Public Structure FILETIME
    <FieldOffset(0)> Public dwLowDateTime As UInteger
    <FieldOffset(0)> Private LongValue As Long
    <FieldOffset(4)> Public dwHighDateTime As UInteger

    Public ReadOnly Property dotNETDate As Date
        Get
        Return Date.FromFileTime(LongValue)
        End Get
    End Property
    Public ReadOnly Property Value() As Long
        Get
        Return LongValue
        End Get
    End Property
    End Structure
The FindFirstFileEx API11/23/2014 3:33:27 PM - imaginarydevelopment@googlemail.com-50.193.161.217The FindFirstFileEx API11/23/2014 3:32:21 PM - -66.194.114.222The FindNextFile API7/17/2012 10:48:26 AM - -79.217.74.81TODO - a short description of this collection of constants4/6/2012 12:59:20 AM - anonymousTODO - a short description of this collection of constants4/6/2012 12:59:20 AM - anonymousTODO - a short description3/16/2007 8:17:31 AM - -63.69.129.2TODO - a short description3/16/2007 8:17:31 AM - -63.69.129.2
```
