
## C# Definition:
```cs
[ComImport]
[Guid("B196B28F-BAB4-101A-B69C-00AA00341D07")]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
interface IClassFactory2 
{
   /// <summary>
   /// the standard create instance (without licence)
   /// </summary>
   /// <param name="unused">must be set to null</param>
   /// <param name="iid">the Guid of the COM class to create</param>
   /// <returns>an instance of the COM class</returns>
   [return: MarshalAs(UnmanagedType.Interface)]
   Object CreateInstance(
     [In, MarshalAs(UnmanagedType.Interface)] Object unused,
     [In, MarshalAs(UnmanagedType.LPStruct)] Guid iid);

   void LockServer(Int32 fLock);

   IntPtr GetLicInfo(); // TODO : an enum called LICINFO

   [return: MarshalAs(UnmanagedType.BStr)]
   String RequestLicKey(
     [In, MarshalAs(UnmanagedType.U4)] int reserved);

   /// <summary>
   /// create an instance of the COM class thanks to a licence key
   /// </summary>
   /// <param name="pUnkOuter">don't know what it is, set to null</param>
   /// <param name="pUnkReserved">must be set to null</param>
   /// <param name="iid">the Guid of the COM class to create</param>
   /// <param name="bstrKey">the licence key</param>
   /// <returns>an instance of the COM class</returns>
   [return: MarshalAs(UnmanagedType.Interface)]
   Object CreateInstanceLic(
     [In, MarshalAs(UnmanagedType.Interface)] object pUnkOuter,
     [In, MarshalAs(UnmanagedType.Interface)] object pUnkReserved,
     [In, MarshalAs(UnmanagedType.LPStruct)] Guid iid, 
     [In, MarshalAs(UnmanagedType.BStr)] string bstrKey); 
}
```

## VB Definition:
```cs
<ComImport()> _
  <Guid("B196B28F-BAB4-101A-B69C-00AA00341D07")> _
  <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _
  Interface IClassFactory2
    ''' <summary>
    ''' the standard create instance (without licence)
    ''' </summary>
    ''' <param name="unused">must be set to null</param>
    ''' <param name="iid">the Guid of the COM class to create</param>
    ''' <returns>an instance of the COM class</returns>
    <[return]: MarshalAs(UnmanagedType.[Interface])> _
    Private Function CreateInstance(_
      <[In](), MarshalAs(UnmanagedType.[Interface])> ByVal unused As Object,_
      <[In](), MarshalAs(UnmanagedType.LPStruct)> ByVal iid As Guid) As Object
    Private Sub LockServer(ByVal fLock As Int32)
    Private Function GetLicInfo() As IntPtr
    ' TODO : an enum called LICINFO
    <[return]: MarshalAs(UnmanagedType.BStr)> _
    Private Function RequestLicKey(<[In](), MarshalAs(UnmanagedType.U4)> ByVal reserved As Integer) As String
    ''' <summary>
    ''' create an instance of the COM class thanks to a licence key
    ''' </summary>
    ''' <param name="pUnkOuter">don't know what it is, set to null</param>
    ''' <param name="pUnkReserved">must be set to null</param>
    ''' <param name="iid">the Guid of the COM class to create</param>
    ''' <param name="bstrKey">the licence key</param>
    ''' <returns>an instance of the COM class</returns>
    <[return]: MarshalAs(UnmanagedType.[Interface])> _
    Private Function CreateInstanceLic(_
      <[In](), MarshalAs(UnmanagedType.[Interface])> ByVal pUnkOuter As Object,_
      <[In](), MarshalAs(UnmanagedType.[Interface])> ByVal pUnkReserved As Object,_
      <[In](), MarshalAs(UnmanagedType.LPStruct)> ByVal iid As Guid,_
      <[In](), MarshalAs(UnmanagedType.BStr)> ByVal bstrKey As String) As Object
  End Interface
```

## Notes:
```cs
String LicenceKey = "haha";
    IClassFactory2 icf2 = Ole32.CoGetClassObject(
        typeof(Interop.MyComLibrary.ComMyLibraryClass).GUID,
        CLSCTX.CLSCTX_LOCAL_SERVER, new System.IntPtr(),
        typeof(IClassFactory2).GUID) as IClassFactory2;
    Interop.MyComLibrary.IMyComClass instance = icf2.CreateInstanceLic(
        null, null, typeof(Interop.MyComLibrary.IMyComClass).GUID, LicenceKey) as Interop.MyComLibrary.IMyComClass;
```
