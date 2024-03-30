
## C# Signature:
```cs
[DllImport("cfgmgr32.dll", SetLastError=true)]
static extern TODO CM_Enumerate_Classes(TODO);
```

## VB Signature:
```cs
<DllImport("cfgmgr32.dll", _
    EntryPoint:="CM_Enumerate_Classes", _
    SetLastError:=True, _
    CharSet:=CharSet.Unicode, _
    ExactSpelling:=True, _
    PreserveSig:=True, _
    CallingConvention:=CallingConvention.Winapi)> _
    Private Shared Function EnumerateClasses( _
    ByVal ClassIndex As Integer, _
    ByRef ClassGuid As GUID, _
    Optional ByVal Flags As Integer = &H0) As Integer
    End Function
```

## Notes:
```cs
Please add some!
```
