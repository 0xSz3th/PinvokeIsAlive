
## C# Definition:
```cs
public enum DOCHOSTUITYPE
{
     DOCHOSTUITYPE_BROWSE = 0,
     DOCHOSTUITYPE_AUTHOR = 1
}

public enum DOCHOSTUIDBLCLK
{
     DOCHOSTUIDBLCLK_DEFAULT = 0,
     DOCHOSTUIDBLCLK_SHOWPROPERTIES = 1,
     DOCHOSTUIDBLCLK_SHOWCODE = 2
}

[Flags()]
public enum DOCHOSTUIFLAG
{
     DOCHOSTUIFLAG_DIALOG = 0x00000001,
     DOCHOSTUIFLAG_DISABLE_HELP_MENU = 0x00000002,
     DOCHOSTUIFLAG_NO3DBORDER = 0x00000004,
     DOCHOSTUIFLAG_SCROLL_NO = 0x00000008,
     DOCHOSTUIFLAG_DISABLE_SCRIPT_INACTIVE = 0x00000010,
     DOCHOSTUIFLAG_OPENNEWWIN = 0x00000020,
     DOCHOSTUIFLAG_DISABLE_OFFSCREEN = 0x00000040,
     DOCHOSTUIFLAG_FLAT_SCROLLBAR = 0x00000080,
     DOCHOSTUIFLAG_DIV_BLOCKDEFAULT = 0x00000100,
     DOCHOSTUIFLAG_ACTIVATE_CLIENTHIT_ONLY = 0x00000200,
     DOCHOSTUIFLAG_OVERRIDEBEHAVIORFACTORY = 0x00000400,
     DOCHOSTUIFLAG_CODEPAGELINKEDFONTS = 0x00000800,
     DOCHOSTUIFLAG_URL_ENCODING_DISABLE_UTF8 = 0x00001000,
     DOCHOSTUIFLAG_URL_ENCODING_ENABLE_UTF8 = 0x00002000,
     DOCHOSTUIFLAG_ENABLE_FORMS_AUTOCOMPLETE = 0x00004000,
     DOCHOSTUIFLAG_ENABLE_INPLACE_NAVIGATION = 0x00010000,
     DOCHOSTUIFLAG_IME_ENABLE_RECONVERSION = 0x00020000,
     DOCHOSTUIFLAG_THEME = 0x00040000,
     DOCHOSTUIFLAG_NOTHEME = 0x00080000,
     DOCHOSTUIFLAG_NOPICS = 0x00100000,
     DOCHOSTUIFLAG_NO3DOUTERBORDER = 0x00200000,
     DOCHOSTUIFLAG_DISABLE_EDIT_NS_FIXUP = 0x400000,
     DOCHOSTUIFLAG_LOCAL_MACHINE_ACCESS_CHECK    = 0x800000,
     DOCHOSTUIFLAG_DISABLE_UNTRUSTEDPROTOCOL    = 0x1000000
}

[ StructLayout( LayoutKind.Sequential )]
public struct DOCHOSTUIINFO
{
     public uint cbSize;
     public uint dwFlags;
     public uint dwDoubleClick;
     [MarshalAs(UnmanagedType.BStr)] public string pchHostCss;
     [MarshalAs(UnmanagedType.BStr)] public string pchHostNS;
}

[StructLayout( LayoutKind.Sequential )]
public struct tagMSG
{
     public IntPtr hwnd;
     public uint message;
     public uint wParam;
     public int lParam;
     public uint time;
     public tagPOINT pt;
}
// Added missing definitions of tagRECT/tagPOINT
[StructLayout(LayoutKind.Sequential, Pack=4)]
public struct tagRECT
{
  public int left;
  public int top;
  public int right;
  public int bottom;
}

[StructLayout(LayoutKind.Sequential, Pack=4)]
public struct tagPOINT
{
  public int x;
  public int y;
}
```

## C# Definition:
```cs
[ComImport()]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
[GuidAttribute("bd3f23c0-d43e-11cf-893b-00aa00bdce1a")]
public interface IDocHostUIHandler
{
     [PreserveSig]
     uint ShowContextMenu(
     uint dwID, 
     ref tagPOINT ppt,
     [MarshalAs(UnmanagedType.IUnknown)]  object pcmdtReserved,
     [MarshalAs(UnmanagedType.IDispatch)] object pdispReserved
     );

     void GetHostInfo(ref DOCHOSTUIINFO pInfo);

     void ShowUI(uint dwID, ref object pActiveObject, ref object pCommandTarget, ref object pFrame, ref object pDoc);

     void HideUI();

     void UpdateUI();

     void EnableModeless(int fEnable);

     void OnDocWindowActivate(int fActivate);

     void OnFrameWindowActivate(int fActivate);

     void ResizeBorder(ref tagRECT prcBorder, int pUIWindow, int fFrameWindow);

     [PreserveSig]
     uint TranslateAccelerator(ref tagMSG lpMsg, ref Guid pguidCmdGroup, uint nCmdID);

     void GetOptionKeyPath([MarshalAs(UnmanagedType.BStr)] ref string pchKey, uint dw);

     uint GetDropTarget(int pDropTarget, ref int ppDropTarget);

     [PreserveSig]
     void GetExternal([MarshalAs(UnmanagedType.IDispatch)] out object ppDispatch);

     [PreserveSig]
     uint TranslateUrl(
     uint dwTranslate, 
     [MarshalAs(UnmanagedType.BStr)] string pchURLIn,
     [MarshalAs(UnmanagedType.BStr)] ref string ppchURLOut
     );

     IDataObject FilterDataObject(IDataObject pDO);
}
```

## VB Definition:
```cs
Imports mshtml
Imports System.Runtime.InteropServices

Public Enum DOCHOSTUITYPE
    DOCHOSTUITYPE_BROWSE = 0
    DOCHOSTUITYPE_AUTHOR = 1
End Enum

Public Enum DOCHOSTUIDBLCLK
    DOCHOSTUIDBLCLK_DEFAULT = 0
     DOCHOSTUIDBLCLK_SHOWPROPERTIES = 1
     DOCHOSTUIDBLCLK_SHOWCODE = 2
End Enum

Public Enum DOCHOSTUIFLAG
    DOCHOSTUIFLAG_DIALOG = &H1
    DOCHOSTUIFLAG_DISABLE_HELP_MENU = &H2
    DOCHOSTUIFLAG_NO3DBORDER = &H4
    DOCHOSTUIFLAG_SCROLL_NO = &H8
    DOCHOSTUIFLAG_DISABLE_SCRIPT_INACTIVE = &H10
    DOCHOSTUIFLAG_OPENNEWWIN = &H20
    DOCHOSTUIFLAG_DISABLE_OFFSCREEN = &H40
    DOCHOSTUIFLAG_FLAT_SCROLLBAR = &H80
    DOCHOSTUIFLAG_DIV_BLOCKDEFAULT = &H100
    DOCHOSTUIFLAG_ACTIVATE_CLIENTHIT_ONLY = &H200
    DOCHOSTUIFLAG_OVERRIDEBEHAVIORFACTORY = &H400
    DOCHOSTUIFLAG_CODEPAGELINKEDFONTS = &H800
    DOCHOSTUIFLAG_URL_ENCODING_DISABLE_UTF8 = &H1000
    DOCHOSTUIFLAG_URL_ENCODING_ENABLE_UTF8 = &H2000
    DOCHOSTUIFLAG_ENABLE_FORMS_AUTOCOMPLETE = &H4000
    DOCHOSTUIFLAG_ENABLE_INPLACE_NAVIGATION = &H10000
    DOCHOSTUIFLAG_IME_ENABLE_RECONVERSION = &H20000
    DOCHOSTUIFLAG_THEME = &H40000
    DOCHOSTUIFLAG_NOTHEME = &H80000
    DOCHOSTUIFLAG_NOPICS = &H100000
    DOCHOSTUIFLAG_NO3DOUTERBORDER = &H200000
    DOCHOSTUIFLAG_DELEGATESIDOFDISPATCH = &H400000
End Enum

<StructLayout(LayoutKind.Sequential)> _
Public Structure DOCHOSTUIINFO
    Public cbSize As Integer
    Public dwFlags As Integer
    Public dwDoubleClick As Integer
    <MarshalAs(UnmanagedType.BStr)> Public pchHostCss As String
    <MarshalAs(UnmanagedType.BStr)> Public pchHostNS As String
End Structure

<StructLayout(LayoutKind.Sequential)> _
Public Structure tagMSG
    Public hwnd As IntPtr
    Public message As Integer
    Public wParam As Integer
    Public lParam As Integer
    Public time As Integer
    Public pt As tagPOINT
End Structure

<ComImport(), InterfaceType(ComInterfaceType.InterfaceIsIUnknown), _
GuidAttribute("bd3f23c0-d43e-11cf-893b-00aa00bdce1a")> _
Public Interface IDocHostUIHandler
    <PreserveSig()> _
    Function ShowContextMenu(ByVal dwID As Integer, ByRef ppt As tagPOINT, _
    <MarshalAs(UnmanagedType.IUnknown)> ByVal pcmdtReserved As Object, _
    <MarshalAs(UnmanagedType.IDispatch)> ByVal pdispReserved As Object) As Integer

    Sub GetHostInfo(ByRef pInfo As DOCHOSTUIINFO)
    Sub ShowUI(ByVal dwID As Integer, ByRef pActiveObjectas As Object, ByRef pCommandTarget As Object, ByRef pFrame As Object, ByRef pDoc As Object)
    Sub HideUI()
    Sub UpdateUI()
    Sub EnableModeless(ByVal fEnable As Integer)
    Sub OnDocWindowActivate(ByVal fActivate As Integer)
    Sub OnFrameWindowActivate(ByVal fActivate As Integer)
    Sub ResizeBorder(ByRef prcBorder As tagRECT, ByVal pUIWindow As Integer, ByVal fRameWindow As Integer)

    <PreserveSig()> _
    Function TranslateAccelerator(ByRef lpMsg As tagMSG, ByRef pguidCmdGroup As Guid, ByVal nCmdID As Integer) As Integer

    Sub GetOptionKeyPath(<MarshalAs(UnmanagedType.BStr)> ByRef pchKey As String, ByVal dw As Integer)
    Function GetDropTarget(ByVal pDropTarget As Integer, ByRef ppDropTarget As Integer) As Integer
    Sub GetExternal(<MarshalAs(UnmanagedType.IDispatch)> ByVal ppDispatch As Object)

    <PreserveSig()> _
    Function TranslateUrl(ByVal dwTranslate As Integer, _
    <MarshalAs(UnmanagedType.BStr)> ByVal pchURLIn As String, _
    <MarshalAs(UnmanagedType.BStr)> ByRef ppchURLOut As String) As Integer

    Function FilterDataObject(ByVal pDO As IDataObject) As IDataObject
End Interface
```
