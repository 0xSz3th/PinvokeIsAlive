
## C# Definition:
```cs
[ComImport]
    [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    [Guid("000214E2-0000-0000-C000-000000000046")]
    public interface IShellBrowser {
    void GetWindow(out IntPtr phwnd);
    void ContextSensitiveHelp(bool fEnterMode);

    void InsertMenusSB(IntPtr IntPtrShared, IntPtr lpMenuWidths);
    void SetMenuSB(IntPtr IntPtrShared, IntPtr holemenuRes, 
               IntPtr IntPtrActiveObject);
    void RemoveMenusSB(IntPtr IntPtrShared);
    void SetStatusTextSB(IntPtr pszStatusText);
    void EnableModelessSB(bool fEnable);
    void TranslateAcceleratorSB(IntPtr pmsg, UInt16 wID);

    void BrowseObject(IntPtr pidl, UInt32 wFlags);
    void GetViewStateStream(UInt32 grfMode, IntPtr ppStrm);
    void GetControlWindow(UInt32 id, out IntPtr lpIntPtr);
    void SendControlMsg(UInt32 id, UInt32 uMsg, UInt32 wParam, UInt32 lParam, IntPtr pret);
    void QueryActiveShellView(ref IShellView ppshv);
    void OnViewWindowActive(IShellView ppshv);
    void SetToolbarItems(IntPtr lpButtons, UInt32 nButtons, UInt32 uFlags);
    }
```

## VB Definition:
```cs
<ComImport> _
<Guid("TODO")> _
'TODO: Insert <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _ if this doesn't derive from IDispatch
Interface IShellBrowser
   TODO
End Interface
```
