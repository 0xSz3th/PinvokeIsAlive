
## C# Signature:
```cs
[DllImport("rasapi32.dll", CharSet=CharSet.Auto, SetLastError=true)]
static extern uint RasGetConnectionStatistics(IntPtr hRasConn, ref RAS_STATS lpStatistics);
```

## VB Signature:
```cs
<DllImport("rasapi32.dll", CharSet:=CharSet:Auto)> _
Public Shared Function RasGetConnectionStatistics( _
     ByVal hRasConn As IntPtr, _
     ByRef lpStatistics As RAS_STATS) As UInt32
End Function
```

## Sample Code:
```cs
RAS_STATS statistics = new RAS_STATS();
statistics.dwSize = Marshal.SizeOf(statistics);
uint retVal = RasGetConnectionStatistics(rasConnectionHandle, ref statistics);
```
