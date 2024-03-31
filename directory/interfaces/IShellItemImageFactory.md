
## C# Definition:
```cs
[ComImportAttribute()]
    [GuidAttribute("bcc18b79-ba16-442f-80c4-8a59c30c463b")]
    [InterfaceTypeAttribute(ComInterfaceType.InterfaceIsIUnknown)]
    public interface IShellItemImageFactory
    {
        void GetImage(
        [In, MarshalAs(UnmanagedType.Struct)] SIZE size,
        [In] SIIGBF flags,
        [Out] out IntPtr phbm);
    }
```

## VB Definition:
```cs
<ComImportAttribute(),  _
    GuidAttribute("bcc18b79-ba16-442f-80c4-8a59c30c463b"),  _
    InterfaceTypeAttribute(ComInterfaceType.InterfaceIsIUnknown)>  _
    Public Interface IShellItemImageFactory    

        Sub GetImage(ByVal size As SIZE, ByVal flags As SIIGBF, ByRef phbm As IntPtr)
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
```
