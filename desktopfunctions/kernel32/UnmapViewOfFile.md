
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true)]
static extern bool UnmapViewOfFile(IntPtr lpBaseAddress);
```

## VB.NET Signature:
```cs
<DllImport("kernel32", setlasterror:=True)> _
    Public Shared Function UnmapViewOfFile(ByVal hBaseAddress As IntPtr) As Boolean
    End Function
```
