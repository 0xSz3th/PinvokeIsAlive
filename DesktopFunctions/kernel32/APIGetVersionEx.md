
## C# Signature:
```cs
[DllImport("kernel32", SetLastError = true)]
private static extern bool GetVersionEx(ref OSVERSIONINFOEX osvi);

[StructLayout(LayoutKind.Sequential)]
private struct OSVERSIONINFOEX
{
    public uint dwOSVersionInfoSize;
    public uint dwMajorVersion;
    public uint dwMinorVersion;
    public uint dwBuildNumber;
    public uint dwPlatformId;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 128)]
    public string szCSDVersion;
    public UInt16 wServicePackMajor;
    public UInt16 wServicePackMinor;
    public UInt16 wSuiteMask;
    public byte wProductType;
    public byte wReserved;
}
```

## VB Signature:
```cs
Private Declare Function GetVersionEx Lib "kernel32.dll" _
    Alias "GetVersionExA" _
    (ByRef lpVersionInformation As OSVERSIONINFOEX) As Boolean
```

## VB Signature:
```cs
<StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Ansi)> _
    Structure OSVERSIONINFOEX
    Public dwOSVersionInfoSize As Integer
    Public dwMajorVersion As Integer
    Public dwMinorVersion As Integer
    Public dwBuildNumber As Integer
    Public dwPlatformId As Integer
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=128)> _
    Public szCSDVersion As String
    Public wServicePackMajor As Integer
    Public wServicePackMinor As Integer
    Public wSuiteMask As Integer
    Public wProductType As Byte
    Public wReserved As Byte
    End Structure 'OSVERSIONINFOEX

    'see if the current process is running on Windows XP
    Public Function IsWinXP() As Boolean

    'returns True if running Windows XP
    Dim osv As New OSVERSIONINFOEX

    osv.dwOSVersionInfoSize = Marshal.SizeOf(osv)

    Dim si As New SYSTEM_INFO

    If GetVersionEx(osv) = 1 Then

        GetSystemInfo(si)

        Return (osv.dwMajorVersion = 5 And osv.dwMinorVersion = 2)
    Else
        Return False
    End If
    End Function

    'see if the current process is running on Windows Vista 
    Public Function IsWinVista() As Boolean

    'returns True if running Windows Vista
    Dim osv As New OSVERSIONINFOEX
    osv.dwOSVersionInfoSize = Marshal.SizeOf(osv)

    If GetVersionEx(osv) = 1 Then
        Return (osv.wProductType = VER_NT_WORKSTATION And osv.dwMajorVersion = 6) 
    Else
        Return False
    End If
    End Function
```

## Tips & Tricks:
```cs
don't forget to set the dwOSVersionInfoSize
```

## Sample Code:
```cs
OSVERSIONINFOEX osVersionInfo = new OSVERSIONINFOEX();
osVersionInfo.dwOSVersionInfoSize = Marshal.SizeOf(osVersionInfo); // don't forget this line, please!
GetVersionEx(ref osVersionInfo);
```
