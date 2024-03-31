
## C# Definition:
```cs
[ComImport, Guid ( "886D8EEB-8CF2-4446-8D02-CDBA1DBDCF99" ), InterfaceType ( ComInterfaceType.InterfaceIsIUnknown )]
interface IPropertyStore
{
    [MethodImpl ( MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime )]
    void GetCount ( [Out] out uint cProps );

    [MethodImpl ( MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime )]
    void GetAt ( [In] uint iProp, out NativeMethods.PROPERTYKEY pkey );

    [MethodImpl ( MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime )]
    void GetValue ( [In] ref NativeMethods.PROPERTYKEY key, out object pv );

    [MethodImpl ( MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime )]
    void SetValue ( [In] ref NativeMethods.PROPERTYKEY key, [In] ref object pv );

    [MethodImpl ( MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime )]
    void Commit ( );
}
```

## VB Definition:
```cs
<ComImport, Guid("886D8EEB-8CF2-4446-8D02-CDBA1DBDCF99"), InterfaceType(ComInterfaceType.InterfaceIsIUnknown)>
Public Interface IPropertyStore
    <MethodImpl(MethodImplOptions.InternalCall, MethodCodeType:=MethodCodeType.Runtime)>
    Sub GetCount(ByRef cProps As UInt32)

    <MethodImpl(MethodImplOptions.InternalCall, MethodCodeType:=MethodCodeType.Runtime)>
    Sub GetAt(ByVal iProp As UInt32, ByRef pkey As NativeMethods.PROPERTYKEY)

    <MethodImpl(MethodImplOptions.InternalCall, MethodCodeType:=MethodCodeType.Runtime)>
    Sub GetValue(ByRef key As NativeMethods.PROPERTYKEY, ByRef pv As Object)

    <MethodImpl(MethodImplOptions.InternalCall, MethodCodeType:=MethodCodeType.Runtime)>
    Sub SetValue(ByRef key As NativeMethods.PROPERTYKEY, ByRef pv As Object)

    <MethodImpl(MethodImplOptions.InternalCall, MethodCodeType:=MethodCodeType.Runtime)>
    Sub Commit()
End Interface
```
