
## C# Signature:
```cs
[DllImport("ntdll.dll", SetLastError=true)]
static extern int RtlGetVersion(ref OSVERSIONINFOEXW versionInfo);
```

## Boo Signature:
```cs
[DllImport("ntdll.dll", SetLastError : true)]
def RtlGetVersion(ref versionInfo as OSVERSIONINFOEXW) as bool:
     pass
```

## User-Defined Types:
```cs
enum PRODUCT_TYPE:
     VER_NT_WORKSTATION = 0x0000001
     VER_NT_DOMAIN_CONTROLLER = 0x0000002
     VER_NT_SERVER = 0x0000003

[StructLayout(LayoutKind.Sequential, CharSet : CharSet.Unicode)]
struct OSVERSIONINFOEXW:
     dwOSVersionInfoSize as int
     dwMajorVersion as int
     dwMinorVersion as int
     dwBuildNumber as int
     dwPlatformId as int
     [MarshalAs(UnmanagedType.ByValTStr, SizeConst : 128)]
     szCSDVersion as string
     wServicePackMajor as UInt16
     wServicePackMinor as UInt16
     wSuiteMask as UInt16
     wProductType as PRODUCT_TYPE
     wReserved as byte
```

## Sample Code:
```cs
var osvi = default(OSVERSIONINFOEXW);
        osvi.dwOSVersionInfoSize = Marshal.SizeOf(typeof(OSVERSIONINFOEXW));
        var result = RtlGetVersion(ref osvi);
        if (result != 0)
        {
           // TODO: Error handling
        }
        else
        {
           return osvi;
        }
```
