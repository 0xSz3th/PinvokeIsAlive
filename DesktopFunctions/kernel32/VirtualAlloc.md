
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true, ExactSpelling=true)]
static extern IntPtr VirtualAllocEx(IntPtr hProcess, IntPtr lpAddress,
   IntPtr dwSize, AllocationType flAllocationType, MemoryProtection flProtect);
```

## C# Signature:
```cs
[DllImport("kernel32")]
  public static extern IntPtr VirtualAlloc(IntPtr lpAddress, uint dwSize, uint flAllocationType, uint flProtect);
```

## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true, ExactSpelling = true)]
    static extern IntPtr VirtualAllocEx(IntPtr hProcess, 
                        IntPtr lpAddress,
                        int dwSize, 
                        AllocationType flAllocationType, 
                        MemoryProtection flProtect);
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll", SetLastError:=True, ExactSpelling:=True)> _
Private Function VirtualAllocEx(ByVal hProcess As IntPtr, ByVal lpAddress As IntPtr, _
     ByVal dwSize As IntPtr, ByVal flAllocationType As UInteger, _
     ByVal flProtect As UInteger) As IntPtr
End Function
```

## VBA Signature:
```cs
Private Declare PtrSafe Function VirtualAlloc Lib "KERNEL32.dll" _
(ByVal lpAddress As LongPtr, ByVal dwSize As LongPtr, ByVal flAllocationType As Long, ByVal flProtect As Long) As LongPtr
```

## Boo Signature:
```cs
[DllImport("kernel32.dll")]
def VirtualAllocEx(hProcess as IntPtr, lpAddress as IntPtr, dwSize as UInt32, flNewProtect as UInt32, lpflOldProtect as UInt32) as IntPtr:
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
```

## Sample Code:
```cs
IntPtr allocatedBaseAddress = VirtualAllocEx(process.Handle, IntPtr.Zero, buffer.Length, AllocationType.Commit | AllocationType.Reserve, MemoryProtection.ExecuteReadWrite);
```
