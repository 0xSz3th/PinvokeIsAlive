
## C# Signature:
```cs
[DllImport("ole32.dll")]
static extern int CoMarshalInterThreadInterfaceInStream([In] ref Guid riid,
   [MarshalAs(UnmanagedType.IUnknown)] object pUnk, out IStream ppStm);
```
