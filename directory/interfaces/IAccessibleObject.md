
## C# Definition:
```cs
public interface IAccessibleObject
    {
    [PreserveSig()]
    int SetAccessibleName([MarshalAs(UnmanagedType.LPTStr)] string pszName);
    }
```

## VB Definition:
```cs
<ComImport()> _
    <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _
    <Guid("95A391C5-9ED4-4C28-8401-AB9E06719E11")> _
    Public Interface IAccessibleObject
         <PreserveSig()> Function SetAccessibleName(<MarshalAs(UnmanagedType.LPWStr)> ByVal pszName As String) As Integer
    End Interface
```
