
## C# Signature:
```cs
[DllImport("ole32.dll")]
static extern int CoRegisterMessageFilter(IMessageFilter lpMessageFilter,
   out IMessageFilter lplpMessageFilter);
```

## VB Signature:
```cs
DllImport("ole32.dll")> _
  <PreserveSig()> _
  Private Shared Function CoRegisterMessageFilter(ByVal lpMessageFilter As IMessageFilter, 
                           ByRef lplpMessageFilter As IMessageFilter) As Integer
```
