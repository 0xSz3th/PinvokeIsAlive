
## C# Signature:
```cs
[DllImport("ntdll.dll", SetLastError=true)]

static extern uint NtTerminateProcess(IntPtr hProcess, int errorStatus);
```

## VB Signature:
```cs
<DllImport("ntdll.dll")>
    Public Shared Function NtTerminateProcess(ByVal hfandle As IntPtr, ByVal ErrorStatus As Integer) As UInteger
    End Function
```

## Boo Signature:
```cs
[DllImport("ntdll.dll", SetLastError : true)]
def NtTerminateProcess(ProcessHandle as IntPtr, ExitStatus as UInt32) as UInt32:
     pass
```
