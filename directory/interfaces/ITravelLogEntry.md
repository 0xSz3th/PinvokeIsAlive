
## C# Definition:
```cs
[ComImport]
[Guid("TODO")]
//TODO: Insert [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)] if this doesn't derive from IDispatch
interface ITravelLogEntry {
   TODO;
}
```

## VB Definition:
```cs
<ComImport(), _
    ComVisible(False), _
    GuidAttribute("7EBFDD85-AD18-11d3-A4C5-00C04F72D6B8"), _
    InterfaceTypeAttribute(ComInterfaceType.InterfaceIsIUnknown)> _
Public Interface IEnumTravelLogEntry

    <PreserveSig()> _
    Function [Next](<[In](), MarshalAs(UnmanagedType.U4)> ByVal cElt As Integer, _
    <Out(), MarshalAs(UnmanagedType.Interface)> ByRef rgElt As ITravelLogEntry, _
    <Out(), MarshalAs(UnmanagedType.U4)> ByRef pcEltFetched As Integer) As Integer

    <PreserveSig()> _
    Function Skip(<[In](), MarshalAs(UnmanagedType.U4)> ByVal cElt As Integer) As Integer

    <PreserveSig()> Function Reset() As Integer

    <PreserveSig()> _
    Function Clone(<Out(), MarshalAs(UnmanagedType.Interface)> ByRef ppEnum As IEnumTravelLogEntry) As Integer

End Interface
```
