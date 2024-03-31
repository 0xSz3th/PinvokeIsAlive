
## C# Definition:
```cs
[ComImport()]
[GuidAttribute("3050f6d0-98b5-11cf-bb82-00aa00bdce0b")]
public interface IDocHostUIHandler2: IDocHostUIHandler
{
     void GetOverrideKeyPath([MarshalAs(UnmanagedType.BStr)] ref string pchKey, uint dw);
}
```

## VB Definition:
```cs
<ComImport> _
<Guid("3050f6d0-98b5-11cf-bb82-00aa00bdce0b")> _
'TODO: Insert <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _ if this doesn't derive from IDispatch
Interface IDocHostUIHandler2
   Inherits IDocHostUIHandler
   Sub GetOverrideKeyPath(<MarshalAs(UnmanagedType.BStr)> ByRef pchKey As String, dw As UInt32)
End Interface
```
