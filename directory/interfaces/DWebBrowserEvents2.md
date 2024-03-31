
## C# Definition:
```cs
[ComImport, SuppressUnmanagedCodeSecurity, InterfaceType(ComInterfaceType.InterfaceIsIDispatch), Guid("34A715A0-6587-11D0-924A-0020AFC7AC4D")]
public interface DWebBrowserEvents2
{
      [DispId(0x66)]
      void StatusTextChange([MarshalAs(UnmanagedType.BStr)] string Text);
      [DispId(0x6c)]
      void ProgressChange(int Progress, int ProgressMax);
      [DispId(0x69)]
      void CommandStateChange(int Command, [MarshalAs(UnmanagedType.VariantBool)] bool Enable);
      [DispId(0x6a)]
      void DownloadBegin();
      [DispId(0x68)]
      void DownloadComplete();
      [DispId(0x71)]
      void TitleChange([MarshalAs(UnmanagedType.BStr)] string Text);
      [DispId(0x70)]
      void PropertyChange([MarshalAs(UnmanagedType.BStr)] string szProperty);
      [DispId(250)]
      void BeforeNavigate2([MarshalAs(UnmanagedType.IDispatch)] object pDisp, [In] ref object URL, [In] ref object Flags, [In] ref object TargetFrameName, [In] ref object PostData, [In] ref object Headers, [In, Out, MarshalAs(UnmanagedType.VariantBool)] ref bool Cancel);
      [DispId(0xfb)]
      void NewWindow2([In, Out, MarshalAs(UnmanagedType.IDispatch)] ref object ppDisp, [In, Out, MarshalAs(UnmanagedType.VariantBool)] ref bool Cancel);
      [DispId(0xfc)]
      void NavigateComplete2([MarshalAs(UnmanagedType.IDispatch)] object pDisp, [In] ref object URL);
      [DispId(0x103)]
      void DocumentComplete([MarshalAs(UnmanagedType.IDispatch)] object pDisp, [In] ref object URL);
      [DispId(0xfd)]
      void OnQuit();
      [DispId(0xfe)]
      void OnVisible([MarshalAs(UnmanagedType.VariantBool)] bool Visible);
      [DispId(0xff)]
      void OnToolBar([MarshalAs(UnmanagedType.VariantBool)] bool ToolBar);
      [DispId(0x100)]
      void OnMenuBar([MarshalAs(UnmanagedType.VariantBool)] bool MenuBar);
      [DispId(0x101)]
      void OnStatusBar([MarshalAs(UnmanagedType.VariantBool)] bool StatusBar);
      [DispId(0x102)]
      void OnFullScreen([MarshalAs(UnmanagedType.VariantBool)] bool FullScreen);
      [DispId(260)]
      void OnTheaterMode([MarshalAs(UnmanagedType.VariantBool)] bool TheaterMode);
      [DispId(0x106)]
      void WindowSetResizable([MarshalAs(UnmanagedType.VariantBool)] bool Resizable);
      [DispId(0x108)]
      void WindowSetLeft(int Left);
      [DispId(0x109)]
      void WindowSetTop(int Top);
      [DispId(0x10a)]
      void WindowSetWidth(int Width);
      [DispId(0x10b)]
      void WindowSetHeight(int Height);
      [DispId(0x107)]
      void WindowClosing([MarshalAs(UnmanagedType.VariantBool)] bool IsChildWindow, [In, Out, MarshalAs(UnmanagedType.VariantBool)] ref bool Cancel);
      [DispId(0x10c)]
      void ClientToHostWindow([In, Out] ref int CX, [In, Out] ref int CY);
      [DispId(0x10d)]
      void SetSecureLockIcon(int SecureLockIcon);
      [DispId(270)]
      void FileDownload([In, Out, MarshalAs(UnmanagedType.VariantBool)] ref bool Cancel);
      [DispId(0x10f)]
      void NavigateError([MarshalAs(UnmanagedType.IDispatch)] object pDisp, [In] ref object URL, [In] ref object Frame, [In] ref object StatusCode, [In, Out, MarshalAs(UnmanagedType.VariantBool)] ref bool Cancel);
      [DispId(0xe1)]
      void PrintTemplateInstantiation([MarshalAs(UnmanagedType.IDispatch)] object pDisp);
      [DispId(0xe2)]
      void PrintTemplateTeardown([MarshalAs(UnmanagedType.IDispatch)] object pDisp);
      [DispId(0xe3)]
      void UpdatePageStatus([MarshalAs(UnmanagedType.IDispatch)] object pDisp, [In] ref object nPage, [In] ref object fDone);
      [DispId(0x110)]
      void PrivacyImpactedStateChange([MarshalAs(UnmanagedType.VariantBool)] bool bImpacted);
      [DispId(0x111)]
      void NewWindow3([In, Out, MarshalAs(UnmanagedType.IDispatch)] ref object ppDisp, [In, Out, MarshalAs(UnmanagedType.VariantBool)] ref bool Cancel, uint dwFlags, [MarshalAs(UnmanagedType.BStr)] string bstrUrlContext, [MarshalAs(UnmanagedType.BStr)] string bstrUrl);
}
```

## VB Definition:
```cs
<ComImport, SuppressUnmanagedCodeSecurity, InterfaceType(ComInterfaceType.InterfaceIsIDispatch), Guid("34A715A0-6587-11D0-924A-0020AFC7AC4D")> _
Public Interface DWebBrowserEvents2
      ' Methods
      <DispId(250)> _
      Sub BeforeNavigate2(<MarshalAs(UnmanagedType.IDispatch)> ByVal pDisp As Object, <In> ByRef URL As Object, <In> ByRef Flags As Object, <In> ByRef TargetFrameName As Object, <In> ByRef PostData As Object, <In> ByRef Headers As Object, <In, Out, MarshalAs(UnmanagedType.VariantBool)> ByRef Cancel As Boolean)
      <DispId(268)> _
      Sub ClientToHostWindow(<In, Out> ByRef CX As Integer, <In, Out> ByRef CY As Integer)
      <DispId(105)> _
      Sub CommandStateChange(ByVal Command As Integer, <MarshalAs(UnmanagedType.VariantBool)> ByVal Enable As Boolean)
      <DispId(259)> _
      Sub DocumentComplete(<MarshalAs(UnmanagedType.IDispatch)> ByVal pDisp As Object, <In> ByRef URL As Object)
      <DispId(106)> _
      Sub DownloadBegin()
      <DispId(104)> _
      Sub DownloadComplete()
      <DispId(270)> _
      Sub FileDownload(<In, Out, MarshalAs(UnmanagedType.VariantBool)> ByRef Cancel As Boolean)
      <DispId(252)> _
      Sub NavigateComplete2(<MarshalAs(UnmanagedType.IDispatch)> ByVal pDisp As Object, <In> ByRef URL As Object)
      <DispId(271)> _
      Sub NavigateError(<MarshalAs(UnmanagedType.IDispatch)> ByVal pDisp As Object, <In> ByRef URL As Object, <In> ByRef Frame As Object, <In> ByRef StatusCode As Object, <In, Out, MarshalAs(UnmanagedType.VariantBool)> ByRef Cancel As Boolean)
      <DispId(251)> _
      Sub NewWindow2(<In, Out, MarshalAs(UnmanagedType.IDispatch)> ByRef ppDisp As Object, <In, Out, MarshalAs(UnmanagedType.VariantBool)> ByRef Cancel As Boolean)
      <DispId(273)> _
      Sub NewWindow3(<In, Out, MarshalAs(UnmanagedType.IDispatch)> ByRef ppDisp As Object, <In, Out, MarshalAs(UnmanagedType.VariantBool)> ByRef Cancel As Boolean, ByVal dwFlags As UInt32, <MarshalAs(UnmanagedType.BStr)> ByVal bstrUrlContext As String, <MarshalAs(UnmanagedType.BStr)> ByVal bstrUrl As String)
      <DispId(258)> _
      Sub OnFullScreen(<MarshalAs(UnmanagedType.VariantBool)> ByVal FullScreen As Boolean)
      <DispId(256)> _
      Sub OnMenuBar(<MarshalAs(UnmanagedType.VariantBool)> ByVal MenuBar As Boolean)
      <DispId(253)> _
      Sub OnQuit()
      <DispId(257)> _
      Sub OnStatusBar(<MarshalAs(UnmanagedType.VariantBool)> ByVal StatusBar As Boolean)
      <DispId(260)> _
      Sub OnTheaterMode(<MarshalAs(UnmanagedType.VariantBool)> ByVal TheaterMode As Boolean)
      <DispId(255)> _
      Sub OnToolBar(<MarshalAs(UnmanagedType.VariantBool)> ByVal ToolBar As Boolean)
      <DispId(254)> _
      Sub OnVisible(<MarshalAs(UnmanagedType.VariantBool)> ByVal Visible As Boolean)
      <DispId(225)> _
      Sub PrintTemplateInstantiation(<MarshalAs(UnmanagedType.IDispatch)> ByVal pDisp As Object)
      <DispId(226)> _
      Sub PrintTemplateTeardown(<MarshalAs(UnmanagedType.IDispatch)> ByVal pDisp As Object)
      <DispId(272)> _
      Sub PrivacyImpactedStateChange(<MarshalAs(UnmanagedType.VariantBool)> ByVal bImpacted As Boolean)
      <DispId(108)> _
      Sub ProgressChange(ByVal Progress As Integer, ByVal ProgressMax As Integer)
      <DispId(112)> _
      Sub PropertyChange(<MarshalAs(UnmanagedType.BStr)> ByVal szProperty As String)
      <DispId(269)> _
      Sub SetSecureLockIcon(ByVal SecureLockIcon As Integer)
      <DispId(102)> _
      Sub StatusTextChange(<MarshalAs(UnmanagedType.BStr)> ByVal [Text] As String)
      <DispId(113)> _
      Sub TitleChange(<MarshalAs(UnmanagedType.BStr)> ByVal [Text] As String)
      <DispId(227)> _
      Sub UpdatePageStatus(<MarshalAs(UnmanagedType.IDispatch)> ByVal pDisp As Object, <In> ByRef nPage As Object, <In> ByRef fDone As Object)
      <DispId(263)> _
      Sub WindowClosing(<MarshalAs(UnmanagedType.VariantBool)> ByVal IsChildWindow As Boolean, <In, Out, MarshalAs(UnmanagedType.VariantBool)> ByRef Cancel As Boolean)
      <DispId(267)> _
      Sub WindowSetHeight(ByVal Height As Integer)
      <DispId(264)> _
      Sub WindowSetLeft(ByVal Left As Integer)
      <DispId(262)> _
      Sub WindowSetResizable(<MarshalAs(UnmanagedType.VariantBool)> ByVal Resizable As Boolean)
      <DispId(265)> _
      Sub WindowSetTop(ByVal Top As Integer)
      <DispId(266)> _
      Sub WindowSetWidth(ByVal Width As Integer)
End Interface
```
