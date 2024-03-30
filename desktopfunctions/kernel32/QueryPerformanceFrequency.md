
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true)]
static extern bool QueryPerformanceFrequency(out long frequency);
```

## VB Signature:
```cs
<DllImport("kernel32.dll", SetLastError:=True)> _
Shared Function QueryPerformanceFrequency(ByRef lpFrequency As Long) As Boolean
End Function
```
