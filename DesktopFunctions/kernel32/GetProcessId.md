
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true)]
public static extern uint GetProcessIdOfThread(IntPtr handle);
```

## VB Signature:
```cs
Declare Function GetProcessIdOfThread Lib "kernel32" (ByVal Thread As IntPtr) As UInt32
```

## Boo Signature:
```cs
[DllImport("kernel32.dll", SetLastError : true)]
def GetProcessId(hProcess as IntPtr) as UInt32:
     pass
```
