
## Boo Signature:
```cs
[DllImport("ntdll.dll", SetLastError : true)]
def RtlCreateProcessParametersEx(
    ref ProcessParameters as IntPtr,
    ref ImagePathName as UNICODE_STRING,
    DllPath as IntPtr,
    ref CurrentDirectory as UNICODE_STRING,
    ref CommandLine as UNICODE_STRING,
    Environment as IntPtr,
    ref WindowTitle as UNICODE_STRING,
    ref DesktopInfo as UNICODE_STRING,
    ShellInfo as IntPtr,
    RuntimeData as IntPtr,
    Flags as UInt32
    ) as UInt32
     pass
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential, Pack : 0)]
struct UNICODE_STRING:
     Length as UInt16
     MaximumLength as UInt16
     Buffer as IntPtr
```
