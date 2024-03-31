
## C# Definition:
```cs
[ComImport, Guid("5e38b83c-8cf1-11d1-bf92-0060081ed811")]
    [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    public interface IEnumWIA_DEV_INFO
    {
    void Next(
        [In] int celt,
        [Out, MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 0)] IWiaPropertyStorage[] rgelt,
        [Out, In] ref int celtFetched);

    void Skip(
        [In] int celt);

    void Reset();

    void Clone(
        [Out, MarshalAs(UnmanagedType.Interface)] out object clonedIEnum);

    void GetCount(
        [Out] out int celt);
    }
```

## VB Definition:
```cs
<ComImport> _
<Guid("TODO")> _
'TODO: Insert <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _ if this doesn't derive from IDispatch
Interface IEnumWIA_DEV_INFO
   TODO
End Interface
```
