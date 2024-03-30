
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool AttachThreadInput(uint idAttach, uint idAttachTo,
   bool fAttach);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Public Shared Function AttachThreadInput(ByVal idAttach As System.UInt32, ByVal idAttachTo As System.UInt32, ByVal fAttach As Boolean) As Boolean
End Function
```
