
## C# Definition:
```cs
[
    ComImport,
    Guid("00000100-0000-0000-C000-000000000046"),
    InterfaceType(ComInterfaceType.InterfaceIsIUnknown)
    ]

    public interface IEnumUnknown
    {
        [PreserveSig]
        int Next(
        [In, MarshalAs(UnmanagedType.U4)] int celt,
        [Out, MarshalAs(UnmanagedType.IUnknown)] out object rgelt,
        [Out, MarshalAs(UnmanagedType.U4)] out int pceltFetched);
        [PreserveSig]
        int Skip([In, MarshalAs(UnmanagedType.U4)] int celt);
        void Reset();
        void Clone(out IEnumUnknown ppenum);
    }
```

## VB Definition:
```cs
<ComImport> _
<Guid("TODO")> _
'TODO: Insert <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _ if this doesn't derive from IDispatch
Interface IEnumUnknown
   TODO
End Interface
```
