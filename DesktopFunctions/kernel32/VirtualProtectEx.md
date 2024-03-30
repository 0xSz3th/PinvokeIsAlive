
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool VirtualProtectEx(IntPtr hProcess, IntPtr lpAddress,
   UIntPtr dwSize, uint flNewProtect, out uint lpflOldProtect);
```

## VB.Net Signature:
```cs
<DllImport("kernel32", CharSet:=CharSet.Auto, SetLastError:=True)> _
    Public Shared Function VirtualProtectEx(ByVal hProcess As IntPtr, ByVal lpAddress As IntPtr, ByVal dwSize As IntPtr, ByVal flNewProtect As UInteger, ByRef lpflOldProtect As UInteger) As Boolean
    End Function
```

## Boo Signature:
```cs
[DllImport("kernel32.dll")]
def VirtualProtectEx(hProcess as IntPtr, lpAddress as IntPtr, dwSize as UInt32, flNewProtect as UInt32, ref lpflOldProtect as UInt32) as bool:
     pass
```

## VB6 Signature:
```cs
Public Declare Function VirtualProtectEx Lib "kernel32" (ByVal hProcess As Long, ByVal lpAddress As Any, ByVal dwSize As Long, ByVal flNewProtect As Long, ByVal lpflOldProtect As Long) As Long
```

## Tips & Tricks:
```cs
In Essential C# 2.0 by Mark Michaelis, it is mentioned ref is to be used for lpflOldProtect rather than out because the callee can ignore the data passed with ref.
```
