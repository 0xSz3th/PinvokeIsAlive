
## C# Signature:
```cs
[DllImport("rasapi32.dll", SetLastError=true)]
static extern uint RasHangUp(IntPtr hRasConn);
```

## VB Signature:
```cs
<DllImport("rasapi32.dll", CharSet:=CharSet:=Auto)> _
Public Shared Function RasHangUp(ByVal hRasConn As IntPtr) As UInt32
End Function
```
