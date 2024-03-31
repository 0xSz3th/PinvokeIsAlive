
## C# Definition:
```cs
[ComImport(),InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
[GuidAttribute("000214e8-0000-0000-c000-000000000046")]
public interface IShellExtInit
{
    [PreserveSig()]
    int Initialize (IntPtr pidlFolder, IntPtr lpdobj, uint /*HKEY*/ hKeyProgID);
}
```

## VB Definition:
```cs
<ComImport(), InterfaceType(ComInterfaceType.InterfaceIsIUnknown),
  GuidAttribute("000214e8-0000-0000-c000-000000000046")> _
Public Interface IShellExtInit
    <PreserveSig()> _
    Function Initialize(ByVal pidlFolder As IntPtr, ByVal lpdobj As IntPtr, ByVal hKeyProgID As IntPtr) As Integer
End Interface 'IShellExtInit
```
