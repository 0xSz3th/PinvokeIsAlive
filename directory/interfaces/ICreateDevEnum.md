
## C# Definition:
```cs
[ComImport]
[Guid(0x29840822, 0x5b84, 0x11d0, 0xbd, 0x3b, 0x00, 0xa0, 0xc9, 0x11, 0xce, 0x86)]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
interface ICreateDevEnum {
   void CreateClassEnumerator(
     ref Guid clsidDeviceClass,

     [Out]
     out IEnumMoniker ppEnumMoniker,

     int dwFlags /*reserved must be 0*/
   );
}
!!!!VB Definition:
<ComImport> _
<Guid("TODO")> _
'TODO: Insert <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _ if this doesn't derive from IDispatch
Interface ICreateDevEnum
   TODO
End Interface
```
