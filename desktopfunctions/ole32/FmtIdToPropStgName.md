
## C# Signature:
```cs
[DllImport("ole32.dll")]
static extern int FmtIdToPropStgName([In] ref Guid pfmtid,
   [Out, MarshalAs(UnmanagedType.LPWStr)] StringBuilder oszName);
```

## VB.Net Signature:
```cs
<DllImport("ole32.dll", preservesig:=False)> _
Public Shared Function FmtIdToPropStgName( _
    <[In]()> ByRef FMTID As Guid, _
        <Out(), MarshalAs(UnmanagedType.LPWStr)> _
    ByVal oszName As StringBuilder) As Integer
End Function
```
