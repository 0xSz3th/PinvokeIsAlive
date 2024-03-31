
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct CEOSVERSIONINFO
{
    public UInt32 dwOSVersionInfoSize;
    public UInt32 dwMajorVersion;
    public UInt32 dwMinorVersion;
    public UInt32 dwBuildNumber;
    public UInt32 dwPlatformId;
    [MarshalAs(UnmanagedType.ByValTStr,SizeConst= 128)]
    public string szCSDVersion;
}
```

## VB Definition:
```cs
Imports System.Runtime.InteropServices

<StructLayout(LayoutKind.Sequential)> _
Public Structure CEOSVERSIONINFO
    Public dwOSVersionInfoSize As UInt32
    Public dwMajorVersion As UInt32
    Public dwMinorVersion As UInt32
    Public dwBuildNumber As UInt32
    Public dwPlatformId As UInt32
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=128)> _
    Public szCSDVersion As String
End Structure
```
