
## Boo Signature:
```cs
[DllImport("ntdll.dll", SetLastError : true)]
def NtQueryVirtualMemory(
     ProcessHandle as IntPtr,
     BaseAddress as IntPtr,
     MemoryInformationClass as MEMORY_INFORMATION_CLASS,
     ref MemoryInformation as MEMORY_BASIC_INFORMATION,
     MemoryInformationLength as UInt32,
     ref ReturnLength as UInt32) as UInt32:
     pass
```

## User-Defined Types:
```cs
enum MEMORY_INFORMATION_CLASS:
     MemoryBasicInformation

struct MEMORY_BASIC_INFORMATION:
     BaseAddress as IntPtr
     AllocationBase as IntPtr
     AllocationProtect as PageAccessProtectionFlags
     RegionSize as IntPtr
     State as StateEnum
     Protect as PageAccessProtectionFlags
     Type as TypeEnum
```
