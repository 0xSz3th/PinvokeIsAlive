
## C# Definition:
```cs
//Code from Hans Passant, http://stackoverflow.com/a/24078693/18192
    [ComImport, InterfaceType(ComInterfaceType.InterfaceIsIUnknown), Guid("0002E000-0000-0000-C000-000000000046")]
    public interface IEnumGUID
    {
        [PreserveSig]
        int Next(uint celt, [Out, MarshalAs(UnmanagedType.LPArray, SizeParamIndex=0)] Guid[] rgelt, out uint pceltFetched);
        [PreserveSig]
        int Skip(uint celt);
        [PreserveSig]
        int Reset();
        void Clone(out IEnumGUID ppenum);
    }
```

## VB Definition:
```cs
'=======================================================
    'Code converted from C# to VB by online service at Telerik (www.telerik.com)
    'Conversion powered by NRefactory, Built and maintained by Todd Anglin and Telerik
    'Converted code has not been tested.
    '=======================================================
    <ComImport, InterfaceType(ComInterfaceType.InterfaceIsIUnknown), Guid("0002E000-0000-0000-C000-000000000046")> _
        Public Interface IEnumGUID
        <PreserveSig> _
        Function [Next](celt As Integer, <Out, MarshalAs(UnmanagedType.LPArray, SizeParamIndex := 0)> rgelt As Guid(), ByRef pceltFetched As Integer) As Integer
        <PreserveSig> _
        Function Skip(celt As Integer) As Integer
        <PreserveSig> _
        Function Reset() As Integer
        Sub Clone(ByRef ppenum As IEnumGUID)
    End Interface
```
