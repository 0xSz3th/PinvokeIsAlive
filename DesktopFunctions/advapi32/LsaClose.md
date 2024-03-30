
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError=true)]
static extern uint LsaClose(IntPtr ObjectHandle);
```

## VB Signature:
```cs
Declare Unicode Function LsaClose Lib "advapi32.dll" (ByVal ObjectHandle As IntPtr) As Int32
```
