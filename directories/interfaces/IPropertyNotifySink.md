
## C# Definition:
```cs
[ComImport]
[Guid("9BFBBC02-EFF1-101A-84ED-00AA00341D07")]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
interface IPropertyNotifySink
{
   int OnChanged(int dispId);

   [PreserveSig]
   int OnRequestEdit(int dispId);
}
```

## VB Definition:
```cs
<ComImport()> _
<Guid("9BFBBC02-EFF1-101A-84ED-00AA00341D07")> _
<InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _
Public Interface iProperyNotifySink
    Interface IPropertyNotifySink

        Function OnChanged(ByVal dispId As Int32) As Int32

        <PreserveSig()> _
        Function OnRequestEdit(ByVal dispId As Int32) As Int32

    End Interface
End Interface
```
