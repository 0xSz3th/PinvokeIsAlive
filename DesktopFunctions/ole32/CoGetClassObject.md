
## C# Signature:
```cs
[DllImport("ole32.dll", CharSet=CharSet.Unicode, ExactSpelling=true, PreserveSig=false)]
[return: MarshalAs(UnmanagedType.Interface)] 
static extern object CoGetClassObject(
   [In, MarshalAs(UnmanagedType.LPStruct)] Guid rclsid, 
   CLSCTX dwClsContext,
   IntPtr pServerInfo, 
   [In, MarshalAs(UnmanagedType.LPStruct)] Guid riid);
```

## VB Signature:
```cs
Declare Unicode Function CoGetClassObject _
    Lib "ole32.dll" _
    Alias "CoGetClassObject" _
    (<[In](), MarshalAs(UnmanagedType.LPStruct)> ByVal rclsid As Guid, _
    ByVal dwClsContext As CLSCTX, _
    ByVal pServerInfo As IntPtr, _
    <[In](), MarshalAs(UnmanagedType.LPStruct)> ByVal riid As Guid) _
    As <MarshalAs(UnmanagedType.Interface)> Object
```
