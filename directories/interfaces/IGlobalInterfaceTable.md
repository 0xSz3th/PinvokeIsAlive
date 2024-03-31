
## C# Definition:
```cs
[
        ComImport,
        InterfaceType(ComInterfaceType.InterfaceIsIUnknown),
        Guid("00000146-0000-0000-C000-000000000046")
    ]
    interface IGlobalInterfaceTable
    {
        uint RegisterInterfaceInGlobal(
                [MarshalAs(UnmanagedType.IUnknown)] object pUnk,
                [In] ref Guid riid);

        void RevokeInterfaceFromGlobal(uint dwCookie);

        [return: MarshalAs(UnmanagedType.IUnknown)]
        object GetInterfaceFromGlobal(uint dwCookie, [In] ref Guid riid);
    }

    [
        ComImport,
        Guid("00000323-0000-0000-C000-000000000046")
    ]
    class StdGlobalInterfaceTable /* : IGlobalInterfaceTable */
    {
    }
```

## VB Definition:
```cs
<ComImport> _
<Guid("TODO")> _
'TODO: Insert <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _ if this doesn't derive from IDispatch
Interface IGlobalInterfaceTable
   TODO
End Interface
```

## Notes:
```cs
IGlobalInterfaceTable pGIT = (IGlobalInterfaceTable) new StdGlobalInterfaceTable();
```
