
## C# Definition:
```cs
[InterfaceTypeAttribute(ComInterfaceType.InterfaceIsIUnknown)]
[ComVisibleAttribute(true)]
[GuidAttribute("0000010F-0000-0000-C000-000000000046")]
[ComImportAttribute()]
public interface IAdviseSink
{
    void OnDataChange(FORMATETC pFormatetc, STGMEDIUM pStgmed);
    void OnViewChange([MarshalAs(UnmanagedType.U4)] int dwAspect, [MarshalAs(UnmanagedType.I4)] int lindex);
    void OnRename([MarshalAs(UnmanagedType.Interface)] object pmk);
    void OnSave();
    void OnClose();
}
```

## VB Definition:
```cs
<ComImport> _
<Guid("TODO")> _
'TODO: Insert <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _ if this doesn't derive from IDispatch
Interface IAdviseSink
   TODO
End Interface
```
