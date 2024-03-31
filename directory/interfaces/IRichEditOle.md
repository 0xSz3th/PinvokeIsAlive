
## C# Definition:
```cs
[ComImport]
[Guid("00020D00-0000-0000-C000-000000000046")]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
interface IRichEditOle {
  void GetClientSite(out IOleClientSite lplpolesite);
[PreserveSig]
  int GetObjectCount();
[PreserveSig]
  int GetLinkCount();
  void GetObject(int iob, ref REOBJECT lpreobject, [MarshalAs(UnmanagedType.U4)] GetObjectOptions flags);
  void InsertObject(REOBJECT lpreobject);
  void ConvertObject(int iob, Guid rclsidNew, string lpstrUserTypeNew);
  void ActivateAs(Guid rclsid, Guid rclsidAs);
  void SetHostNames(string lpstrContainerApp, string lpstrContainerObj);
  void SetLinkAvailable(int iob, bool fAvailable);
  void SetDvaspect(int iob, uint dvaspect);
  void HandsOffStorage(int iob);
  void SaveCompleted(int iob, IStorage lpstg);
  void InPlaceDeactivate();
  void ContextSensitiveHelp(bool fEnterMode);
  void GetClipboardData(ref CHARRANGE lpchrg, [MarshalAs(UnmanagedType.U4)] GetClipboardDataFlags reco, out IDataObject lplpdataobj);
  void ImportDataObject(IDataObject lpdataobj, int cf, IntPtr hMetaPict);
}
```

## VB Definition:
```cs
<ComImport> _
<Guid("TODO")> _
<InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _
Interface IRichEditOle
   TODO
End Interface
```
