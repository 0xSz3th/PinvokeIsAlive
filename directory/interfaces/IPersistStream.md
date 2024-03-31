
## C# Definition:
```cs
[ComImport]
[Guid("7FD52380-4E07-101B-AE2D-08002B2EC713")]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
interface IPersistStreamInit {
    int GetClassID (out Guid pClassID);
    void GetSizeMax ([OutAttribute] ulong[] pcbSize);    
    void InitNew ();
    int IsDirty ();    
    void Load ([InAttribute] IStream pstm);
    void Save ([InAttribute] IStream pstm, [InAttribute] int fClearDirty);
}
```

## VB Definition:
```cs
<ComImport> _
<Guid("7FD52380-4E07-101B-AE2D-08002B2EC713")> _
'TODO: Insert <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _ if this doesn't derive from IDispatch
Interface IPersistStreamInit
   TODO
End Interface
```
