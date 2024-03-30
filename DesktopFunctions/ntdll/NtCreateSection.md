
## C# Signature:
```cs
[DllImport("ntdll.dll", SetLastError = true, ExactSpelling = true)]
static extern UInt32 NtCreateSection(
    ref IntPtr SectionHandle,
    UInt32 DesiredAccess,
    IntPtr ObjectAttributes,
    ref UInt32 MaximumSize,
    UInt32 SectionPageProtection,
    UInt32 AllocationAttributes,
    IntPtr FileHandle);
```

## Boo Signature:
```cs
[DllImport("ntdll.dll")]
def NtCreateSection(ref SectionHandle as IntPtr, DesiredAccess as UInt32, ObjectAttributes as IntPtr, ref MaximumSize as LARGE_INTEGER, SectionPageProtection as UInt32, AllocationAttributes as UInt32, FileHandle as IntPtr) as UInt32:
     pass
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Explicit, Size:8)]
struct LARGE_INTEGER:
     [FieldOffset(0)]QuadPart as UInt64
     [FieldOffset(0)]LowPart as UInt32
     [FieldOffset(4)]HighPart as UInt32
```

## C# Code:
```cs
//Below is the sample code for creating Section with RWX permissions.
  IntPtr SectionHandle = IntPtr.Zero;
  uint MaximumSize = 2048;
  private static uint SEC_COMMIT = 0x08000000;
  private static uint SECTION_MAP_WRITE = 0x0002;
  private static uint SECTION_MAP_READ = 0x0004;
  private static uint SECTION_MAP_EXECUTE = 0x0008;
  private static uint SECTION_ALL_ACCESS = SECTION_MAP_WRITE | SECTION_MAP_READ | SECTION_MAP_EXECUTE;
  uint res = NtCreateSection(ref SectionHandle, SECTION_ALL_ACCESS, IntPtr.Zero, ref MaximumSize, EXECUTE_READ_WRITE, SEC_COMMIT,IntPtr.Zero);
  // res = 0 indicates a successful creation of section
```
