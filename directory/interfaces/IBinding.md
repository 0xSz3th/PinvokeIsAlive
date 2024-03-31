
## C# Definition:
```cs
[ComImport, 
    Guid("79EAC9C0-BAF9-11CE-8C82-00AA004BA90B"), 
    InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    public interface IBinding
    {
        [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType=MethodCodeType.Runtime)]
        void Abort();
        [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType=MethodCodeType.Runtime)]
        void Suspend();
        [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType=MethodCodeType.Runtime)]
        void Resume();
        [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType=MethodCodeType.Runtime)]
        void SetPriority([In] int nPriority);
        [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType=MethodCodeType.Runtime)]
        void GetPriority(out int pnPriority);
        [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType=MethodCodeType.Runtime)]
        void GetBindResult(out Guid pclsidProtocol, out uint pdwResult, [MarshalAs(UnmanagedType.LPWStr)] out string pszResult, [In, Out] ref uint dwReserved);
    }
```

## VB.NET Definition:
```cs
<ComImport(), Guid("79EAC9C0-BAF9-11CE-8C82-00AA004BA90B"), InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _
Public Interface IBinding
    <MethodImpl(MethodImplOptions.InternalCall, MethodCodeType:=MethodCodeType.Runtime)> _
    Sub Abort()

    <MethodImpl(MethodImplOptions.InternalCall, MethodCodeType:=MethodCodeType.Runtime)> _
    Sub Suspend()

    <MethodImpl(MethodImplOptions.InternalCall, MethodCodeType:=MethodCodeType.Runtime)> _
    Sub [Resume]()

    <MethodImpl(MethodImplOptions.InternalCall, MethodCodeType:=MethodCodeType.Runtime)> _
    Sub SetPriority(<[In]()> ByVal nPriority As Integer)

    <MethodImpl(MethodImplOptions.InternalCall, MethodCodeType:=MethodCodeType.Runtime)> _
    Sub GetPriority(ByRef pnPriority As Integer)

    <MethodImpl(MethodImplOptions.InternalCall, MethodCodeType:=MethodCodeType.Runtime)> _
    Sub GetBindResult(ByRef pclsidProtocol As Guid, ByRef pdwResult As UInteger, <MarshalAs(UnmanagedType.LPWStr)> ByRef pszResult As String, <[In](), [Out]()> ByRef dwReserved As UInteger)

End Interface
```
