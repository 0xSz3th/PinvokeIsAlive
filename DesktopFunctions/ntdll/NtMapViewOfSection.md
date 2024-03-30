
## C# Signature:
```cs
[DllImport("ntdll.dll", SetLastError=true)]
static extern uint NtMapViewOfSection(
    IntPtr SectionHandle,
    IntPtr ProcessHandle,
    ref IntPtr BaseAddress,
    UIntPtr ZeroBits,
    UIntPtr CommitSize,
    out ulong SectionOffset,
    out uint ViewSize,
    uint InheritDisposition,
    uint AllocationType,
    uint Win32Protect);
```

## VB Signature:
```cs
Declare Function NtMapViewOfSection Lib "ntdll.dll" (TODO) As TODO
```

## Boo Signature:
```cs
[DllImport("ntdll.dll")]
def NtMapViewOfSection(SectionHandle as IntPtr, ProcessHandle as IntPtr, ref BaseAddress as IntPtr, ZeroBits as UIntPtr, CommitSize as UIntPtr, ref SectionOffset as ulong, ref ViewSize as uint, InheritDisposition as uint, AllocationType as uint, Win32Protect as uint):
     pass
```
