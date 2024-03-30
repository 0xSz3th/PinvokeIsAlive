
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true, ExactSpelling=true)]
static extern IntPtr VirtualAllocEx(IntPtr hProcess, IntPtr lpAddress,
   uint dwSize, uint flAllocationType, uint flProtect);
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll", SetLastError:=True, ExactSpelling:=True)> _
Private Function VirtualAllocEx(ByVal hProcess As IntPtr, ByVal lpAddress As IntPtr, _
     ByVal dwSize As UInteger, ByVal flAllocationType As UInteger, _
     ByVal flProtect As UInteger) As IntPtr
End Function
```

## Boo Signature:
```cs
[DllImport("kernel32.dll", SetLastError : true, ExactSpelling : true)]
static def VirtualAllocEx(hProcess as IntPtr, lpAddress as IntPtr, dwSize as Int32, flAllocationType as AllocationType, flProtect as MemoryProtection) as IntPtr:
     pass
```

## User-Defined Types:
```cs
[Flags]
public enum AllocationType
{
     Commit = 0x1000,
     Reserve = 0x2000,
     Decommit = 0x4000,
     Release = 0x8000,
     Reset = 0x80000,
     Physical = 0x400000,
     TopDown = 0x100000,
     WriteWatch = 0x200000,
     LargePages = 0x20000000
}

[Flags]
public enum MemoryProtection
{
     Execute = 0x10,
     ExecuteRead = 0x20,
     ExecuteReadWrite = 0x40,
     ExecuteWriteCopy = 0x80,
     NoAccess = 0x01,
     ReadOnly = 0x02,
     ReadWrite = 0x04,
     WriteCopy = 0x08,
     GuardModifierflag = 0x100,
     NoCacheModifierflag = 0x200,
     WriteCombineModifierflag = 0x400
}

[Flags]
enum AllocationType:
     Commit = 0x1000
     Reserve = 0x2000
     Decommit = 0x4000
     Release = 0x8000
     Reset = 0x80000
     Physical = 0x400000
     TopDown = 0x100000
     WriteWatch = 0x200000
     LargePages = 0x20000000

[Flags]
enum MemoryProtection:
     Execute = 0x10
     ExecuteRead = 0x20
     ExecuteReadWrite = 0x40
     ExecuteWriteCopy = 0x80
     NoAccess = 0x01
     ReadOnly = 0x02
     ReadWrite = 0x04
     WriteCopy = 0x08
     GuardModifierflag = 0x100
     NoCacheModifierflag = 0x200
     WriteCombineModifierflag = 0x400
```
