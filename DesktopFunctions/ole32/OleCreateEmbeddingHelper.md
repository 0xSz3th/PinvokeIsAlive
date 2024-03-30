
## C# Signature:
```cs
[DllImport("ole32.dll")]
static extern int OleCreateEmbeddingHelper([In] ref Guid clsid,
   [MarshalAs(UnmanagedType.IUnknown)] object pUnkOuter, uint flags,
   IClassFactory pCF, [In] ref Guid riid, [MarshalAs(UnmanagedType.IUnknown)]
   out object ppvObj);
```
