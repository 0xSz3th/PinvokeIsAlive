
## C# Signature:
```cs
[DllImport("setupapi.dll", SetLastError=true)]
static extern TODO SetupDiOpenClassRegKeyEx(TODO);
```

## VB Signature:
```cs
<DllImport("setupapi.dll", _
    EntryPoint:="SetupDiOpenClassRegKeyExW", _
    SetLastError:=True, _
    CharSet:=CharSet.Unicode, _
    ExactSpelling:=True, _
    PreserveSig:=True, _
    CallingConvention:=CallingConvention.Winapi)> _
    Private Shared Function SetupDiOpenClassRegKeyEx( _
    ByRef ClassGuid As GUID, _
    ByVal samDesired As Integer, _
    ByVal Flags As Integer, _
    ByVal MachineName As Integer, _
    ByVal Reserved As Integer) As Integer
    End Function
```
