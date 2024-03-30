
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool Process32Next(IntPtr hSnapshot, ref PROCESSENTRY32 lppe);
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll")> _
Private Shared Function Process32Next(ByVal hSnapshot As IntPtr, ByRef lppe As PROCESSENTRY32) As Boolean
End Function
```
