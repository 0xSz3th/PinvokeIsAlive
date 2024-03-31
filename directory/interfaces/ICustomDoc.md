
## C# Definition:
```cs
using System.Runtime.InteropServices;
[ComImport, InterfaceType(ComInterfaceType.InterfaceIsIUnknown), Guid("3050F3F0-98B5-11CF-BB82-00AA00BDCE0B")]
public interface ICustomDoc
{
    void SetUIHandler([In, MarshalAs(UnmanagedType.Interface)] IDocHostUIHandler pUIHandler);
}
```

## VB Definition:
```cs
Imports System.Runtime.InteropServices

<ComImport(), InterfaceType(ComInterfaceType.InterfaceIsIUnknown), _
Guid("3050f3f0-98b5-11cf-bb82-00aa00bdce0b")> _
Interface ICustomDoc
    <PreserveSig()> _
    Sub SetUIHandler(ByVal pUIHandler As IDocHostUIHandler)
End Interface
```
