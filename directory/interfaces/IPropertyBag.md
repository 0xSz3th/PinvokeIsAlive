
## C# Definition:
```cs
[ComImport]
[Guid("55272A00-42CB-11CE-8135-00AA004BB851"),
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
public interface IPropertyBag
{
   [PreserveSig]
   int Read(
     [In, MarshalAs(UnmanagedType.LPWStr)] string pszPropName,
     [Out, MarshalAs(UnmanagedType.Struct)] out object pVar,
     [In] IErrorLog pErrorLog
   );

   [PreserveSig]
   int Write(
     [In, MarshalAs(UnmanagedType.LPWStr)] string pszPropName,
     [In, MarshalAs(UnmanagedType.Struct)] ref object pVar
   );
}
```

## VB Definition:
```cs
<ComImport> _
<Guid("TODO")> _
<InterfaceType(ComInterfaceType.InterfaceIsIUnknown)>
Interface IPropertyBag
   TODO
End Interface
```
