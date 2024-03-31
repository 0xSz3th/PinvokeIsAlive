
## C# Definition:
```cs
[ComImport, Guid("0000010c-0000-0000-c000-000000000046"),
InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
public interface IPersist
{
    [PreserveSig]
    void GetClassID(out Guid pClassID);
}
```

## VB Definition:
```cs
#Region "IPersist Interface Definition"
<ComImport(), Guid("0000010c-0000-0000-c000-000000000046"), _
InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _
Public Interface IPersist

    <PreserveSig()> Sub GetClassID(ByRef pClassID As Guid)

End Interface
#End Region
```
