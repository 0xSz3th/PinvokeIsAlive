
## C# Signature:
```cs
[DllImport("ole32.dll")]
static extern int OleCreate([In] ref Guid rclsid, [In] ref Guid riid,
   uint renderopt, [In] ref FORMATETC pFormatEtc, IOleClientSite pClientSite,
   IStorage pStg, [MarshalAs(UnmanagedType.IUnknown)] out object ppvObj);
```
