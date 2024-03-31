
## C# Definition:
```cs
[GuidAttribute("0000010d-0000-0000-C000-000000000046")]
[InterfaceTypeAttribute(ComInterfaceType.InterfaceIsIUnknown)]
[ComImportAttribute()]
public interface IViewObject
{
    void Draw([MarshalAs(UnmanagedType.U4)] int dwDrawAspect, int lindex, IntPtr pvAspect, DVTARGETDEVICE ptd, IntPtr hdcTargetDev, IntPtr hdcDraw, COMRECT lprcBounds, COMRECT lprcWBounds, IntPtr pfnContinue, int dwContinue);
    int GetColorSet([MarshalAs(UnmanagedType.U4)] int dwDrawAspect, int lindex, IntPtr pvAspect, DVTARGETDEVICE ptd, IntPtr hicTargetDev, out tagLOGPALETTE ppColorSet);
    int Freeze([MarshalAs(UnmanagedType.U4)] int dwDrawAspect, int lindex, IntPtr pvAspect, out IntPtr pdwFreeze);
    int Unfreeze([MarshalAs(UnmanagedType.U4)] int dwFreeze);
    int SetAdvise([MarshalAs(UnmanagedType.U4)] int aspects, [MarshalAs(UnmanagedType.U4)] int advf, [MarshalAs(UnmanagedType.Interface)] IAdviseSink pAdvSink);
    void GetAdvise([MarshalAs(UnmanagedType.LPArray)] out int[] paspects, [MarshalAs(UnmanagedType.LPArray)] out int[] advf, [MarshalAs(UnmanagedType.LPArray)] out IAdviseSink[] pAdvSink);
}
```

## VB Definition:
```cs
<ComImport(), Guid("0000010D-0000-0000-C000-000000000046"), InterfaceType(CShort(1)), ComConversionLoss()> _
Public Interface IViewObject
    Sub Draw(<MarshalAs(UnmanagedType.U4)> ByVal dwDrawAspect As UInt32, ByVal lindex As Integer, ByVal pvAspect As IntPtr, <[In]()> ByVal ptd As IntPtr, ByVal hdcTargetDev As IntPtr, ByVal hdcDraw As IntPtr, <MarshalAs(UnmanagedType.Struct)> ByRef lprcBounds As _RECTL, <[In]()> ByVal lprcWBounds As IntPtr, ByVal pfnContinue As IntPtr, <MarshalAs(UnmanagedType.U4)> ByVal dwContinue As UInt32)

    Sub GetColorSet(<[In]()> ByVal dwDrawAspect As UInteger, <[In]()> ByVal lindex As Integer, <[In]()> ByVal pvAspect As UInteger, <[In]()> ByRef ptd As tagDVTARGETDEVICE, <[In]()> ByVal hicTargetDev As UInteger, <Out()> ByVal ppColorSet As IntPtr)

    Sub Freeze(<[In]()> ByVal dwDrawAspect As UInteger, <[In]()> ByVal lindex As Integer, <[In]()> ByVal pvAspect As UInteger, ByRef pdwFreeze As UInteger)

    Sub Unfreeze(<[In]()> ByVal dwFreeze As UInteger)

    Sub SetAdvise(<[In]()> ByVal aspects As UInteger, <[In]()> ByVal advf As UInteger, <[In](), MarshalAs(UnmanagedType.[Interface])> ByVal pAdvSink As IAdviseSink)

    Sub GetAdvise(ByRef pAspects As UInteger, ByRef pAdvf As UInteger, <MarshalAs(UnmanagedType.[Interface])> ByRef ppAdvSink As IAdviseSink)
End Interface
```
