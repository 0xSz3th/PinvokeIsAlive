
## C# Signature:
```cs
[ComVisible(false)]
    [ComImport, InterfaceType(ComInterfaceType.InterfaceIsIUnknown), Guid("00000000-0000-0000-C000-000000000046")]
    public interface IUnknown
    {
    IntPtr QueryInterface(ref Guid riid);

    [PreserveSig]
    UInt32 AddRef();

    [PreserveSig]
    UInt32 Release();
    }
```

## VB Signature:
```cs
<ComVisible(False)> _
<ComImport()> _
<InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _
<Guid("00000000-0000-0000-C000-000000000046")> _
Public Interface IUnknown
     Function QueryInterface(ByRef riid As Guid) As IntPtr

     <PreserveSig()> _
     Function AddRef() As Integer

     <PreserveSig()> _
     Function Release() As Integer
End Interface
```
