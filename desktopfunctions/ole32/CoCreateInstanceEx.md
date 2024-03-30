
## C# Signature:
```cs
[DllImport("ole32.dll", CharSet=CharSet.Unicode, ExactSpelling=true, PreserveSig=false)]
static extern void CoCreateInstanceEx(
   [In, MarshalAs(UnmanagedType.LPStruct)] Guid rclsid,
   [MarshalAs(UnmanagedType.IUnknown)] object pUnkOuter, 
   CLSCTX dwClsCtx,
   IntPtr pServerInfo, 
   uint cmq, 
   [In, Out] MULTI_QI[] pResults);
```

## Alternative Managed API:
```cs
Guid CLSID_ShellDesktop = new Guid("00021400-0000-0000-C000-000000000046");
Type shellDesktopType = Type.GetTypeFromCLSID(CLSID_ShellDesktop, true); // (Guid, serverName, throwOnError)
object shellDesktop = Activator.CreateInstance(shellDesktopType);
```
