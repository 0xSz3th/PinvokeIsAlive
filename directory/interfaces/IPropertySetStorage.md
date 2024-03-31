
## C# Definition:
```cs
[ComImport]
    [Guid("0000013A-0000-0000-C000-000000000046")]
    [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    public interface IPropertySetStorage
    {
        [PreserveSig]
        int Create(
        [In, MarshalAs(UnmanagedType.Struct)] ref System.Guid rfmtid,
        [In] IntPtr pclsid,
        [In] int grfFlags,
        [In] int grfMode,
        ref IPropertyStorage propertyStorage);

        [PreserveSig]
        int Open(
        [In, MarshalAs(UnmanagedType.Struct)] ref System.Guid rfmtid,
        [In] int grfMode,
        [Out] IPropertyStorage propertyStorage);
    }
```
