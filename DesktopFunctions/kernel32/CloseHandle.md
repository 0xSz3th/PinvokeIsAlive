
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true)]
[ReliabilityContract(Consistency.WillNotCorruptState, Cer.Success)]
[SuppressUnmanagedCodeSecurity]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool CloseHandle(IntPtr hObject);
```

## VB .NET Signature:
```cs
<DllImport("kernel32.dll", SetLastError:=True)> _
<ReliabilityContract(Consistency.WillNotCorruptState, Cer.Success)> _
<SuppressUnmanagedCodeSecurity> _
Public Shared Function CloseHandle(ByVal hObject As IntPtr) As <MarshalAs(UnmanagedType.Bool)> Boolean
End Function

Declare Auto Function CloseHandle Lib "kernel32.dll" (ByVal hObject As IntPtr) As Boolean
Declare Function CloseHandle Lib "kernel32" Alias "CloseHandle" (ByVal hObject As Integer) As Integer
```

## Boo Signature:
```cs
[DllImport("kernel32", SetLastError : true)]
def CloseHandle(hObject as IntPtr) as bool:
     pass
```

## Tips & Tricks:
```cs
static extern unsafe bool CloseHandle(
        IntPtr hObject   // handle to object
        );
```

## Sample Code:
```cs
hMapFile = CreateFileMapping(INVALID_HANDLE_VALUE, 0, PAGE_READWRITE, 0, 4096, "mIRC")
CloseHandle(hMapFile)
```
