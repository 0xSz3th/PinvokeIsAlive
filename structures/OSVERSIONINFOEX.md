
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Ansi)]  
struct OSVERSIONINFOEX {
   public int dwOSVersionInfoSize;  
   public int dwMajorVersion;  
   public int dwMinorVersion;  
   public int dwBuildNumber;  
   public int dwPlatformId;
   [MarshalAs(UnmanagedType.ByValTStr, SizeConst=128)]
   public string szCSDVersion;
   public UInt16 wServicePackMajor;  
   public UInt16 wServicePackMinor;  
   public UInt16 wSuiteMask;
   public byte wProductType;  
   public byte wReserved;
```

## VB Definition:
```cs
Public dwOSVersionInfoSize As Integer
   Public dwMajorVersion As Integer
   Public dwMinorVersion As Integer
   Public dwBuildNumber As Integer
   Public dwPlatformId As Integer
   <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=128)> _
   Public szCSDVersion As String
   Public wServicePackMajor As UInt16
   Public wServicePackMinor As UInt16
   Public wSuiteMask As UInt16
   Public wProductType As Byte
   Public wReserved As Byte
```
