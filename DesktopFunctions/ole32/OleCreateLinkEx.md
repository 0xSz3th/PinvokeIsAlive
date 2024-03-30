
## C# Signature:
```cs
[DllImport("ole32.dll")]
static extern int OleCreateLinkEx(UCOMIMoniker pmkLinkSrc, [In] ref Guid riid,
   uint dwFlags, uint renderopt, uint cFormats, uint rgAdvf, FORMATETC []
   rgFormatEtc, IAdviseSink pAdviseSink, [Out] uint [] rgdwConnection,
   IOleClientSite pClientSite, IStorage pStg,
   [MarshalAs(UnmanagedType.IUnknown)] out object ppvObj);
```
