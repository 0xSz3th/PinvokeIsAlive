
## C# Definition:
```cs
[ComImport]
[Guid("79EAC9E3-BAF9-11CE-8C82-00AA004BA90B")]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
interface IInternetProtocolRoot {
    [PreserveSig]
    int Start(
      [MarshalAs(UnmanagedType.LPWStr)] string szUrl,
      [MarshalAs(UnmanagedType.Interface)] IInternetProtocolSink protocolSink,
      IInternetBindInfo bindInfo,
      [MarshalAs(UnmanagedType.I4)] int grfPI,
      IntPtr dwReserved);

    [PreserveSig]
    int Continue([In] ref PROTOCOLDATA protocolData);

    [PreserveSig]
    int Abort(int hrReason, int options);

    [PreserveSig]
    int Terminate(int options);

    [PreserveSig]
    int Suspend();

    [PreserveSig]
    int Resume();
}
```

## VB Definition:
```cs
<ComImport> _
<Guid("79EAC9E3-BAF9-11CE-8C82-00AA004BA90B")> _
<InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _
Interface IInternetProtocolRoot
   TODO
End Interface
```
