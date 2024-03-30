
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

## C# Definition (with Enums):
```cs
[StructLayout(LayoutKind.Sequential)]
  struct OSVERSIONINFOEX
  {
    public uint dwOSVersionInfoSize;
    public uint dwMajorVersion;
    public uint dwMinorVersion;
    public uint dwBuildNumber;
    public uint dwPlatformId;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 128)] public string szCSDVersion;
    public ushort wServicePackMajor;
    public ushort wServicePackMinor;
    public SuiteMask wSuiteMask;
    public ProductType wProductType;
    public byte wReserved;
  }

  enum ProductType : byte
  {
    VER_NT_DOMAIN_CONTROLLER = 0x0000002,
    VER_NT_SERVER = 0x0000003,
    VER_NT_WORKSTATION = 0x0000001,
  }

  [Flags]
  enum SuiteMask : ushort
  {
    VER_SUITE_BACKOFFICE = 0x00000004,
    VER_SUITE_BLADE = 0x00000400,
    VER_SUITE_COMPUTE_SERVER = 0x00004000,
    VER_SUITE_DATACENTER = 0x00000080,
    VER_SUITE_ENTERPRISE = 0x00000002,
    VER_SUITE_EMBEDDEDNT = 0x00000040,
    VER_SUITE_PERSONAL = 0x00000200,
    VER_SUITE_SINGLEUSERTS = 0x00000100,
    VER_SUITE_SMALLBUSINESS = 0x00000001,
    VER_SUITE_SMALLBUSINESS_RESTRICTED = 0x00000020,
    VER_SUITE_STORAGE_SERVER = 0x00002000,
    VER_SUITE_TERMINAL = 0x00000010,
    VER_SUITE_WH_SERVER = 0x00008000,
  }
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
