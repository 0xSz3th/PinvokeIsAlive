
## C# Signature:
```cs
[DllImport("ole32.dll")]
static extern int OleLoad(IStorage pStg, [In] ref Guid riid, IOleClientSite
   pClientSite, [MarshalAs(UnmanagedType.IUnknown)] out object ppvObj);
```
