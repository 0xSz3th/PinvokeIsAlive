
## C# Signature:
```cs
[DllImport("ole32.dll", ExactSpelling=true, PreserveSig=false)]
static extern void WriteClassStg(
    IStorage pStg, 
    [In, MarshalAs(UnmanagedType.LPStruct)] Guid rclsid);
```
