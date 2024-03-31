
## C# Definition:
```cs
[ComImport, Guid ( "B63EA76D-1F85-456F-A19C-48159EFA858B" ), InterfaceType ( ComInterfaceType.InterfaceIsIUnknown )]
interface IShellItemArray
{
    // Not supported: IBindCtx
    [MethodImpl ( MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime )]
    void BindToHandler ( [In, MarshalAs ( UnmanagedType.Interface )] IntPtr pbc, [In] ref Guid rbhid,
                 [In] ref Guid riid, out IntPtr ppvOut );

    [MethodImpl ( MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime )]
    void GetPropertyStore ( [In] int Flags, [In] ref Guid riid, out IntPtr ppv );

    [MethodImpl ( MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime )]
    void GetPropertyDescriptionList ( [In] ref NativeMethods.PROPERTYKEY keyType, [In] ref Guid riid, out IntPtr ppv );

    [MethodImpl ( MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime )]
    void GetAttributes ( [In] NativeMethods.SIATTRIBFLAGS dwAttribFlags, [In] uint sfgaoMask, out uint psfgaoAttribs );

    [MethodImpl ( MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime )]
    void GetCount ( out uint pdwNumItems );

    [MethodImpl ( MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime )]
    void GetItemAt ( [In] uint dwIndex, [MarshalAs ( UnmanagedType.Interface )] out IShellItem ppsi );

    // Not supported: IEnumShellItems (will use GetCount and GetItemAt instead)
    [MethodImpl ( MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime )]
    void EnumItems ( [MarshalAs ( UnmanagedType.Interface )] out IntPtr ppenumShellItems );
}
```

## VB Definition:
```cs
<PreserveSig()> _
    Function BindToHandler(<[In](), MarshalAs(UnmanagedType.[Interface])> pbc As IntPtr, <[In]()> rbhid As Guid, <[In]()> riid As Guid, ByRef ppvOut As IntPtr) As Integer

    <PreserveSig()> _
    Function GetPropertyStore(<[In]()> Flags As Integer, <[In]()> riid As Guid, ByRef ppv As IntPtr) As Integer

    <PreserveSig()> _
    Function GetPropertyDescriptionList(<[In]()> keyType As PROPERTYKEY, <[In]()> riid As Guid, ByRef ppv As IntPtr) As Integer

    <PreserveSig()> _
    Function GetAttributes(<[In]()> dwAttribFlags As SIATTRIBFLAGS, <[In]()> sfgaoMask As SFGAO, ByRef psfgaoAttribs As SFGAO) As Integer

    <PreserveSig()> _
    Function GetCount(ByRef pdwNumItems As UInteger) As Integer

    <PreserveSig()> _
    Function GetItemAt(<[In]()> dwIndex As UInteger, <MarshalAs(UnmanagedType.[Interface])> ByRef ppsi As IShellItem) As Integer

    <PreserveSig()> _
    Function EnumItems(<MarshalAs(UnmanagedType.[Interface])> ByRef ppenumShellItems As IEnumShellItems) As Integer
```

## VB Definition:
```cs
Public fmtid As Guid
    Public pid As UInteger
```

## VB Definition:
```cs
[AND] = 1
    APPCOMPAT = 3
    [OR] = 2
```
