
## C# Definition:
```cs
[ComImport,
    ComVisible(false),
    InterfaceType(ComInterfaceType.InterfaceIsIUnknown), 
    Guid("00000001-0000-0000-C000-000000000046")]
    public interface IClassFactory
    {
    void CreateInstance([MarshalAs(UnmanagedType.IUnknown)] object pUnkOuter, [MarshalAs(UnmanagedType.LPStruct)] Guid riid, out IntPtr ppvObject);
    void LockServer([MarshalAs(UnmanagedType.Bool)] bool fLock);
    }
```

## VB Definition:
```cs
<ComVisible(False), _
  ComImport(), _
  InterfaceType(ComInterfaceType.InterfaceIsIUnknown), _
  Guid("00000001-0000-0000-C000-000000000046")> _
  Public Interface IClassFactory
    Sub CreateInstance(ByVal pUnkOuter As IntPtr, ByRef riid As Guid, <Out()> ByVal ppvObject As IntPtr)
    Sub LockServer(ByVal fLock As Boolean)
  End Interface
```
