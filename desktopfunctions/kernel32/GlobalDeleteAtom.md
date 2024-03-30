
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true, ExactSpelling=true)]
static extern ushort GlobalDeleteAtom(ushort nAtom);
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll", SetLastError:=True, CharSet:=CharSet.Auto)> _
Private Shared Function GlobalDeleteAtom( _
     ByVal nAtom As UShort) As UShort
End Function
```
