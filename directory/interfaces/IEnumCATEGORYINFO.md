
## C# Definition:
```cs
[ComImport, Guid("0002E011-0000-0000-C000-000000000046"), InterfaceType(ComInterfaceType.InterfaceIsIUnknown), ComVisible(false)]
    public interface IEnumCATEGORYINFO
    {
        int Next(int celt, [Out, In, MarshalAs(UnmanagedType.LPArray, SizeParamIndex=0)]CATEGORYINFO[] rgelt);
        void Skip(int celt);
        void Reset();
        [return: MarshalAs(UnmanagedType.Interface)]
        IEnumCATEGORYINFO Clone();
    }
```

## VB Definition:
```cs
<ComImport> _
<Guid("TODO")> _
'TODO: Insert <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _ if this doesn't derive from IDispatch
Interface IEnumCATEGORYINFO
   TODO
End Interface
```
