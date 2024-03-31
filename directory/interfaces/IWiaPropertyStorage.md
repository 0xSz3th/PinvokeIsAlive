
## C# Definition:
```cs
[ComImport, Guid("98B5E8A0-29CC-491a-AAC0-E6DB4FDCCEB6")]
    [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    public interface IWiaPropertyStorage
    {
    void ReadMultiple(
        [In] int cpspec,
        [In, MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 0)] PROPSPEC[] rgpspec,
        [Out, MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 0)] object[] rgpropvar);

    void WriteMultiple(
        [In] int cpspec,
        [In, MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 0)] PROPSPEC[] rgpspec,
        [In, MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 0)] object[] rgpropvar,
        [In] uint propidNameFirst);

    void DeleteMultiple(
        [In] int cpspec,
        [In, MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 0)] PROPSPEC[] rgpspec);

    void ReadPropertyNames(
        [In] int cpropid,
        [In, MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 0)] uint[] rgpropid,
        [Out, MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 0)] IntPtr[] rglpwstrName);

    void WritePropertyNames(
        [In] int cpropid,
        [In, MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 0)] uint[] rgpropid,
        [In, MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 0)] IntPtr[] rglpwstrName);

    void DeletePropertyNames(
        [In] int cpropid,
        [In, MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 0)] uint[] rgpropid);

    void Commit(
        [In] int grfCommitFlags);

    void Revert();

    void Enum(
        [Out, MarshalAs(UnmanagedType.Interface)] out object iEnum);

    void SetTimes(
        [In] ref FILETIME pctime,
        [In] ref FILETIME patime,
        [In] ref FILETIME pmtime);

    void SetClass(
        [In] ref Guid clsid);

    void Stat(
        [Out, MarshalAs(UnmanagedType.LPStruct)] out STATPROPSETSTG pstatpsstg);

    void GetPropertyAttributes(
        [In] int cpspec,
        [In, MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 0)] PROPSPEC[] rgpspec,
        [Out, MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 0)] uint[] rgflags,
        [Out, MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 0)] object[] rgpropvar);

    void GetCount(
        [Out] out int nNumProps);

    void GetPropertyStream(
        [Out] out Guid guidCompatibilityId,
        [Out, MarshalAs(UnmanagedType.Interface)] out object iStream);

    void SetPropertyStream(
        [In] ref Guid guidCompatibilityId,
        [In, MarshalAs(UnmanagedType.Interface)] object iStream);
    }
```

## VB Definition:
```cs
<ComImport> _
<Guid("TODO")> _
'TODO: Insert <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _ if this doesn't derive from IDispatch
Interface IWiaPropertyStorage
   TODO
End Interface
```
