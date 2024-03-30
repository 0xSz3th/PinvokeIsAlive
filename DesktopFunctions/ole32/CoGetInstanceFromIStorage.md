
## C# Signature:
```cs
[DllImport("ole32.dll")]
static extern int CoGetInstanceFromIStorage(IntPtr pServerInfo, [In] ref Guid
   pclsid, [MarshalAs(UnmanagedType.IUnknown)] object pUnkOuter, uint dwClsCtx,
   IStorage pstg, uint cmq, MULTI_QI [] rgmqResults);
```
