
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
static extern uint ResumeThread(IntPtr hThread);
```

## VB Signature:
```cs
<DllImport("kernel32.dll")> _
Shared Function ResumeThread(hThread As IntPtr) As UInt32
End Function
```

## Boo Signature:
```cs
[DllImport("kernel32.dll")]
def ResumeThread(threadHandle as IntPtr) as int:
     pass
```
