
## C# Definition:
```cs
[ComImport]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
[Guid("43826d1e-e718-42ee-bc55-a1e261c37bfe")]
public interface IShellItem {
    void BindToHandler(IntPtr pbc, 
        [MarshalAs(UnmanagedType.LPStruct)]Guid bhid, 
        [MarshalAs(UnmanagedType.LPStruct)]Guid riid, 
        out IntPtr ppv);

    void GetParent(out IShellItem ppsi);

    void GetDisplayName(SIGDN sigdnName, out IntPtr ppszName);

    void GetAttributes(uint sfgaoMask, out uint psfgaoAttribs);

    void Compare(IShellItem psi, uint hint, out int piOrder);
};
```

## VB Definition:
```cs
<ComImport()> _
<Guid("43826d1e-e718-42ee-bc55-a1e261c37bfe")> _
<InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _
Public Interface IShellItem
    Sub BindToHandler(ByVal pbc As IntPtr, _
        <MarshalAs(UnmanagedType.LPStruct)> ByVal bhid As Guid, _
        <MarshalAs(UnmanagedType.LPStruct)> ByVal riid As Guid, _
        ByRef ppv As IntPtr)

    Sub GetParent(ByRef ppsi As IShellItem)

    Sub GetDisplayName(ByVal sigdnName As SIGDN, ByRef ppszName As IntPtr)

    Sub GetAttributes(ByVal sfgaoMask As UInt32, ByRef psfgaoAttribs As UInt32)

    Sub Compare(ByVal psi As IShellItem, ByVal hint As UInt32, ByRef piOrder As Integer)
End Interface
```

## Notes:
```cs
IShellItem ppsi = null;
    IntPtr hbitmap = IntPtr.Zero;
    // GUID of IShellItem.
    Guid uuid = new Guid("43826d1e-e718-42ee-bc55-a1e261c37bfe");
    SHCreateItemFromParsingName(filename, IntPtr.Zero, uuid, out ppsi);
    ((IShellItemImageFactory)ppsi).GetImage(new SIZE(256, 256), 0x0, out hbitmap);

    //Alternatively one does not need IShellItem - this works on Win10
    IShellItemImageFactory ppsiif = null;
    IntPtr hbitmap = IntPtr.Zero;
    SHCreateItemFromParsingName(filename, IntPtr.Zero, new Guid("bcc18b79-ba16-442f-80c4-8a59c30c463b"), out ppsiif);
    ppsiif.GetImage(new SIZE(256, 256), SIIGBF.SIIGBF_BIGGERSIZEOK | SIIGBF.SIIGBF_THUMBNAILONLY, out hbitmap);
    var image = Image.FromHbitmap(hbitmap);
    DeleteObject(hbitmap);
```
