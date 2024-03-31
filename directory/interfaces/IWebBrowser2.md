
## C# Definition:
```cs
[ComImport, Guid("D30C1661-CDAF-11D0-8A3E-00C04FC9E26E"), TypeLibType((short)0x1050), DefaultMember("Name"), SuppressUnmanagedCodeSecurity]
    public interface IWebBrowser2 : IWebBrowserApp
    {
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(100)]
    void GoBack();
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x65)]
    void GoForward();
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x66)]
    void GoHome();
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x67)]
    void GoSearch();
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x68)]
    void Navigate([In, MarshalAs(UnmanagedType.BStr)] string URL, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object Flags, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object TargetFrameName, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object PostData, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object Headers);
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(-550)]
    void Refresh();
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x69)]
    void Refresh2([In, Optional, MarshalAs(UnmanagedType.Struct)] ref object Level);
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x6a)]
    void Stop();
    [DispId(200)]
    object Application { [return: MarshalAs(UnmanagedType.IDispatch)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(200)] get; }
    [DispId(0xc9)]
    object Parent { [return: MarshalAs(UnmanagedType.IDispatch)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xc9)] get; }
    [DispId(0xca)]
    object Container { [return: MarshalAs(UnmanagedType.IDispatch)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xca)] get; }
    [DispId(0xcb)]
    object Document { [return: MarshalAs(UnmanagedType.IDispatch)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xcb)] get; }
    [DispId(0xcc)]
    bool TopLevelContainer { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xcc)] get; }
    [DispId(0xcd)]
    string Type { [return: MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xcd)] get; }
    [DispId(0xce)]
    int Left { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xce)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xce)] set; }
    [DispId(0xcf)]
    int Top { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xcf)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xcf)] set; }
    [DispId(0xd0)]
    int Width { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xd0)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xd0)] set; }
    [DispId(0xd1)]
    int Height { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xd1)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xd1)] set; }
    [DispId(210)]
    string LocationName { [return: MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(210)] get; }
    [DispId(0xd3)]
    string LocationURL { [return: MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xd3)] get; }
    [DispId(0xd4)]
    bool Busy { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xd4)] get; }
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(300)]
    void Quit();
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x12d)]
    void ClientToWindow([In, Out] ref int pcx, [In, Out] ref int pcy);
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x12e)]
    void PutProperty([In, MarshalAs(UnmanagedType.BStr)] string Property, [In, MarshalAs(UnmanagedType.Struct)] object vtValue);
    [return: MarshalAs(UnmanagedType.Struct)]
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x12f)]
    object GetProperty([In, MarshalAs(UnmanagedType.BStr)] string Property);
    [DispId(0)]
    string Name { [return: MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0)] get; }
    [DispId(-515)]
    int HWND { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(-515)] get; }
    [DispId(400)]
    string FullName { [return: MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(400)] get; }
    [DispId(0x191)]
    string Path { [return: MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x191)] get; }
    [DispId(0x192)]
    bool Visible { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x192)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x192)] set; }
    [DispId(0x193)]
    bool StatusBar { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x193)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x193)] set; }
    [DispId(0x194)]
    string StatusText { [return: MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x194)] get; [param: In, MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x194)] set; }
    [DispId(0x195)]
    int ToolBar { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x195)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x195)] set; }
    [DispId(0x196)]
    bool MenuBar { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x196)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x196)] set; }
    [DispId(0x197)]
    bool FullScreen { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x197)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x197)] set; }
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(500)]
    void Navigate2([In, MarshalAs(UnmanagedType.Struct)] ref object URL, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object Flags, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object TargetFrameName, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object PostData, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object Headers);
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x1f5)]
    OLECMDF QueryStatusWB([In] OLECMDID cmdID);
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x1f6)]
    void ExecWB([In] OLECMDID cmdID, [In] OLECMDEXECOPT cmdexecopt, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object pvaIn, [In, Out, Optional, MarshalAs(UnmanagedType.Struct)] ref object pvaOut);
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x1f7)]
    void ShowBrowserBar([In, MarshalAs(UnmanagedType.Struct)] ref object pvaClsid, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object pvarShow, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object pvarSize);
    [DispId(-525)]
    tagREADYSTATE ReadyState { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(-525), TypeLibFunc((short)4)] get; }
    [DispId(550)]
    bool Offline { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(550)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(550)] set; }
    [DispId(0x227)]
    bool Silent { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x227)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x227)] set; }
    [DispId(0x228)]
    bool RegisterAsBrowser { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x228)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x228)] set; }
    [DispId(0x229)]
    bool RegisterAsDropTarget { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x229)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x229)] set; }
    [DispId(0x22a)]
    bool TheaterMode { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x22a)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x22a)] set; }
    [DispId(0x22b)]
    bool AddressBar { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x22b)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x22b)] set; }
    [DispId(0x22c)]
    bool Resizable { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x22c)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x22c)] set; }
    }

    [ComImport, Guid("0002DF05-0000-0000-C000-000000000046"), TypeLibType((short)0x1050), DefaultMember("Name"), SuppressUnmanagedCodeSecurity]
    public interface IWebBrowserApp : IWebBrowser
    {
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(100)]
    void GoBack();
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x65)]
    void GoForward();
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x66)]
    void GoHome();
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x67)]
    void GoSearch();
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x68)]
    void Navigate([In, MarshalAs(UnmanagedType.BStr)] string URL, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object Flags, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object TargetFrameName, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object PostData, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object Headers);
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(-550)]
    void Refresh();
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x69)]
    void Refresh2([In, Optional, MarshalAs(UnmanagedType.Struct)] ref object Level);
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x6a)]
    void Stop();
    [DispId(200)]
    object Application { [return: MarshalAs(UnmanagedType.IDispatch)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(200)] get; }
    [DispId(0xc9)]
    object Parent { [return: MarshalAs(UnmanagedType.IDispatch)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xc9)] get; }
    [DispId(0xca)]
    object Container { [return: MarshalAs(UnmanagedType.IDispatch)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xca)] get; }
    [DispId(0xcb)]
    object Document { [return: MarshalAs(UnmanagedType.IDispatch)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xcb)] get; }
    [DispId(0xcc)]
    bool TopLevelContainer { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xcc)] get; }
    [DispId(0xcd)]
    string Type { [return: MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xcd)] get; }
    [DispId(0xce)]
    int Left { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xce)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xce)] set; }
    [DispId(0xcf)]
    int Top { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xcf)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xcf)] set; }
    [DispId(0xd0)]
    int Width { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xd0)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xd0)] set; }
    [DispId(0xd1)]
    int Height { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xd1)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xd1)] set; }
    [DispId(210)]
    string LocationName { [return: MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(210)] get; }
    [DispId(0xd3)]
    string LocationURL { [return: MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xd3)] get; }
    [DispId(0xd4)]
    bool Busy { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xd4)] get; }
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(300)]
    void Quit();
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x12d)]
    void ClientToWindow([In, Out] ref int pcx, [In, Out] ref int pcy);
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x12e)]
    void PutProperty([In, MarshalAs(UnmanagedType.BStr)] string Property, [In, MarshalAs(UnmanagedType.Struct)] object vtValue);
    [return: MarshalAs(UnmanagedType.Struct)]
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x12f)]
    object GetProperty([In, MarshalAs(UnmanagedType.BStr)] string Property);
    [DispId(0)]
    string Name { [return: MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0)] get; }
    [DispId(-515)]
    int HWND { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(-515)] get; }
    [DispId(400)]
    string FullName { [return: MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(400)] get; }
    [DispId(0x191)]
    string Path { [return: MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x191)] get; }
    [DispId(0x192)]
    bool Visible { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x192)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x192)] set; }
    [DispId(0x193)]
    bool StatusBar { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x193)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x193)] set; }
    [DispId(0x194)]
    string StatusText { [return: MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x194)] get; [param: In, MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x194)] set; }
    [DispId(0x195)]
    int ToolBar { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x195)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x195)] set; }
    [DispId(0x196)]
    bool MenuBar { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x196)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x196)] set; }
    [DispId(0x197)]
    bool FullScreen { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x197)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x197)] set; }
    }

    [ComImport, TypeLibType((short)0x1050), Guid("EAB22AC1-30C1-11CF-A7EB-0000C05BAE0B"), SuppressUnmanagedCodeSecurity]
    public interface IWebBrowser
    {
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(100)]
    void GoBack();
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x65)]
    void GoForward();
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x66)]
    void GoHome();
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x67)]
    void GoSearch();
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x68)]
    void Navigate([In, MarshalAs(UnmanagedType.BStr)] string URL, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object Flags, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object TargetFrameName, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object PostData, [In, Optional, MarshalAs(UnmanagedType.Struct)] ref object Headers);
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(-550)]
    void Refresh();
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x69)]
    void Refresh2([In, Optional, MarshalAs(UnmanagedType.Struct)] ref object Level);
    [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0x6a)]
    void Stop();
    [DispId(200)]
    object Application { [return: MarshalAs(UnmanagedType.IDispatch)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(200)] get; }
    [DispId(0xc9)]
    object Parent { [return: MarshalAs(UnmanagedType.IDispatch)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xc9)] get; }
    [DispId(0xca)]
    object Container { [return: MarshalAs(UnmanagedType.IDispatch)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xca)] get; }
    [DispId(0xcb)]
    object Document { [return: MarshalAs(UnmanagedType.IDispatch)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xcb)] get; }
    [DispId(0xcc)]
    bool TopLevelContainer { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xcc)] get; }
    [DispId(0xcd)]
    string Type { [return: MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xcd)] get; }
    [DispId(0xce)]
    int Left { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xce)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xce)] set; }
    [DispId(0xcf)]
    int Top { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xcf)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xcf)] set; }
    [DispId(0xd0)]
    int Width { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xd0)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xd0)] set; }
    [DispId(0xd1)]
    int Height { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xd1)] get; [param: In] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xd1)] set; }
    [DispId(210)]
    string LocationName { [return: MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(210)] get; }
    [DispId(0xd3)]
    string LocationURL { [return: MarshalAs(UnmanagedType.BStr)] [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xd3)] get; }
    [DispId(0xd4)]
    bool Busy { [MethodImpl(MethodImplOptions.InternalCall, MethodCodeType = MethodCodeType.Runtime), DispId(0xd4)] get; }
    }
```

## VB Definition:
```cs
<ComImport(), Guid("D30C1661-CDAF-11D0-8A3E-00C04FC9E26E"), InterfaceType(ComInterfaceType.InterfaceIsIDispatch), DefaultMember("Name"), SuppressUnmanagedCodeSecurity()> _
    Public Interface IWebBrowser2
    ' Methods
    <DispId(301)> _
    Sub ClientToWindow(<[In](), Out()> ByRef pcx As Integer, <[In](), Out()> ByRef pcy As Integer)
    <DispId(502)> _
    Sub ExecWB(ByVal cmdID As OLECMDID, ByVal cmdexecopt As OLECMDEXECOPT, <[In]()> ByRef pvaIn As Object, <[In](), Out()> ByRef pvaOut As Object)
    <DispId(303)> _
    Function GetProperty(<MarshalAs(UnmanagedType.BStr)> ByVal [Property] As String) As Object
    <DispId(100)> _
    Sub GoBack()
    <DispId(101)> _
    Sub GoForward()
    <DispId(102)> _
    Sub GoHome()
    <DispId(103)> _
    Sub GoSearch()
    <DispId(104)> _
    Sub Navigate(<MarshalAs(UnmanagedType.BStr)> ByVal URL As String, <[In]()> ByRef Flags As Object, <[In]()> ByRef TargetFrameName As Object, <[In]()> ByRef PostData As Object, <[In]()> ByRef Headers As Object)
    <DispId(500)> _
    Sub Navigate2(<[In]()> ByRef URL As Object, <[In]()> ByRef Flags As Object, <[In]()> ByRef TargetFrameName As Object, <[In]()> ByRef PostData As Object, <[In]()> ByRef Headers As Object)
    <DispId(302)> _
    Sub PutProperty(<MarshalAs(UnmanagedType.BStr)> ByVal [Property] As String, ByVal vtValue As Object)
    <DispId(501)> _
    Function QueryStatusWB(ByVal cmdID As OLECMDID) As OLECMDF
    <DispId(300)> _
    Sub Quit()
    <DispId(-550)> _
    Sub Refresh()
    <DispId(105)> _
    Sub Refresh2(<[In]()> ByRef Level As Object)
    <DispId(503)> _
    Sub ShowBrowserBar(<[In]()> ByRef pvaClsid As Object, <[In]()> ByRef pvarShow As Object, <[In]()> ByRef pvarSize As Object)
    <DispId(106)> _
    Sub [Stop]()

    ' Properties
    Property AddressBar() As <MarshalAs(UnmanagedType.VariantBool)> Boolean
    ReadOnly Property Application() As <MarshalAs(UnmanagedType.IDispatch)> Object
    ReadOnly Property Busy() As <MarshalAs(UnmanagedType.VariantBool)> Boolean
    ReadOnly Property Container() As <MarshalAs(UnmanagedType.IDispatch)> Object
    ReadOnly Property Document() As <MarshalAs(UnmanagedType.IDispatch)> Object
    ReadOnly Property FullName() As <MarshalAs(UnmanagedType.BStr)> String
    Property FullScreen() As <MarshalAs(UnmanagedType.VariantBool)> Boolean
    Property Height() As Integer
    ReadOnly Property HWND() As Integer
    Property Left() As Integer
    ReadOnly Property LocationName() As <MarshalAs(UnmanagedType.BStr)> String
    ReadOnly Property LocationURL() As <MarshalAs(UnmanagedType.BStr)> String
    Property MenuBar() As <MarshalAs(UnmanagedType.VariantBool)> Boolean
    ReadOnly Property Name() As <MarshalAs(UnmanagedType.BStr)> String
    Property Offline() As <MarshalAs(UnmanagedType.VariantBool)> Boolean
    ReadOnly Property Parent() As <MarshalAs(UnmanagedType.IDispatch)> Object
    ReadOnly Property Path() As <MarshalAs(UnmanagedType.BStr)> String
    ReadOnly Property ReadyState() As tagREADYSTATE
    Property RegisterAsBrowser() As <MarshalAs(UnmanagedType.VariantBool)> Boolean
    Property RegisterAsDropTarget() As <MarshalAs(UnmanagedType.VariantBool)> Boolean
    Property Resizable() As <MarshalAs(UnmanagedType.VariantBool)> Boolean
    Property Silent() As <MarshalAs(UnmanagedType.VariantBool)> Boolean
    Property StatusBar() As <MarshalAs(UnmanagedType.VariantBool)> Boolean
    Property StatusText() As <MarshalAs(UnmanagedType.BStr)> String
    Property TheaterMode() As <MarshalAs(UnmanagedType.VariantBool)> Boolean
    Property ToolBar() As Integer
    Property Top() As Integer
    ReadOnly Property TopLevelContainer() As <MarshalAs(UnmanagedType.VariantBool)> Boolean
    ReadOnly Property Type() As <MarshalAs(UnmanagedType.BStr)> String
    Property Visible() As <MarshalAs(UnmanagedType.VariantBool)> Boolean
    Property Width() As Integer
    End Interface
```
