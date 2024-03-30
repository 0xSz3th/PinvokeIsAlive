
## C# Signature:
```cs
[DllImport("uxtheme", ExactSpelling=true, CharSet=CharSet.Unicode)]
public extern static Int32 DrawThemeText(IntPtr hTheme, IntPtr hdc, int iPartId, int iStateId, String text, int textLength, UInt32 textFlags, UInt32 textFlags2, ref RECT pRect);
```

## VB .NET Signature:
```cs
<DllImport("uxtheme", ExactSpelling := True, CharSet := CharSet.Unicode)> _
Public Shared Function DrawThemeText(ByVal hTheme As IntPtr, ByVal hdc As IntPtr, ByVal iPartId As Integer, ByVal iStateId As Integer, ByVal text As String, ByVal textLength As Integer, ByVal textFlags As UInt32, ByVal textFlags2 As UInt32, ByRef pRect As RECT) As Int32
End Function
```

## Sample Code:
```cs
Imports System.Runtime.InteropServices

    ' Make sure Themes are enabled in the application
    Public Sub New()
        MyBase.New()

        ' Enable WindowsXP Themes without a manifest file
        System.Windows.Forms.Application.EnableVisualStyles()
        System.Windows.Forms.Application.DoEvents()

        ' This call is required by the Windows Form Designer.
        InitializeComponent()

        ' Add any initialization after the InitializeComponent() call
    End Sub
```

## Sample Code:
```cs
' P/Invoke events
    <DllImport("Comctl32.dll", ExactSpelling:=True, CallingConvention:=CallingConvention.Cdecl, CharSet:=CharSet.Unicode)> _
    Private Overloads Shared Function DllGetVersion(ByRef pdvi As DLLVERSIONINFO) As Integer
    End Function

    <StructLayout(LayoutKind.Sequential)> _
    Private Structure DLLVERSIONINFO
        Friend cbSize As Integer
        Friend dwMajorVersion As Integer
        Friend dwMinorVersion As Integer
        Friend dwBuildNumber As Integer
        Friend dwPlatformID As Integer
    End Structure

    <DllImport("UxTheme.dll", ExactSpelling:=True, CallingConvention:=CallingConvention.Cdecl, CharSet:=CharSet.Unicode)> _
    Public Overloads Shared Function OpenThemeData(ByVal hwnd As IntPtr, <MarshalAs(UnmanagedType.LPTStr)> ByVal pszClassList As String) As IntPtr
    End Function

    <DllImport("UxTheme.dll", ExactSpelling:=True, CallingConvention:=CallingConvention.Cdecl, CharSet:=CharSet.Unicode)> _
    Public Overloads Shared Function CloseThemeData(ByVal htheme As IntPtr) As Integer
    End Function

    <DllImport("UxTheme.dll", ExactSpelling:=True, CallingConvention:=CallingConvention.Cdecl, CharSet:=CharSet.Unicode)> _
    Public Overloads Shared Function DrawThemeText(ByVal hTheme As IntPtr, ByVal hdc As IntPtr, ByVal iPartId As Integer, ByVal iStateId As Integer,  <MarshalAs(UnmanagedType.LPTStr)> ByVal pszText As String, ByVal iCharCount As Integer, ByVal dwTextFlag As DrawTextFlags, ByVal dwTextFlags2 As Integer, ByRef pRect As Rectangle) As Integer
    End Function

    Public Enum DrawTextFlags
        DT_TOP = &H0
        DT_LEFT = &H0
        DT_CENTER = &H1
        DT_RIGHT = &H2
        DT_VCENTER = &H4
        DT_BOTTOM = &H8
        DT_WORDBREAK = &H10
        DT_SINGLELINE = &H20
          DT_EXPANDTABS = &H40
        DT_TABSTOP = &H80
        DT_NOCLIP = &H100
        DT_EXTERNALLEADING = &H200
        DT_CALCRECT = &H400
        DT_NOPREFIX = &H800
        DT_INTERNAL = &H1000
        DT_EDITCONTROL = &H2000
        DT_PATH_ELLIPSIS = &H4000
        DT_END_ELLIPSIS = &H8000
        DT_MODIFYSTRING = &H10000
        DT_RTLREADING = &H20000
        DT_WORD_ELLIPSIS = &H40000
        DT_NOFULLWIDTHCHARBREAK = &H80000
        DT_HIDEPREFIX = &H100000
        DT_PREFIXONLY = &H200000
    End Enum

    Public Enum UX_ThemeClass
    Window
    Button
    Rebar
    Toolbar
    Status
    Menu
    Listview
    Header
    Progress
    Tab
    Trackbar
    Tooltip
    Treeview
    Spin
    Page
    ScrollBar
    Edit
    Combobox
    Clock
    TrayNotify
    Taskbar
    Taskband
    StartPanel
    Explorerbar
    Menuband
    Globals
    End Enum

    Public Enum UX_ThemePart As Integer
    'Public Enum UxThemeWindowParts
    WP_CAPTION = 1
    WP_SMALLCAPTION = 2
    WP_MINCAPTION = 3
    WP_SMALLMINCAPTION = 4
    WP_MAXCAPTION = 5
    WP_SMALLMAXCAPTION = 6
    WP_FRAMELEFT = 7
    WP_FRAMERIGHT = 8
    WP_FRAMEBOTTOM = 9
    WP_SMALLFRAMELEFT = 10
    WP_SMALLFRAMERIGHT = 11
    WP_SMALLFRAMEBOTTOM = 12
    '' //---- window frame buttons ----
    WP_SYSBUTTON = 13
    WP_MDISYSBUTTON = 14
    WP_MINBUTTON = 15
    WP_MDIMINBUTTON = 16
    WP_MAXBUTTON = 17
    WP_CLOSEBUTTON = 18
    WP_SMALLCLOSEBUTTON = 19
    WP_MDICLOSEBUTTON = 20
    WP_RESTOREBUTTON = 21
    WP_MDIRESTOREBUTTON = 22
    WP_HELPBUTTON = 23
    WP_MDIHELPBUTTON = 24
    '' //---- scrollbars
    WP_HORZSCROLL = 25
    WP_HORZTHUMB = 26
    WP_VERTSCROLL = 27
    WP_VERTTHUMB = 28
    '' //---- dialog ----
    WP_DIALOG = 29
    '' //---- hit-test templates ---
    WP_CAPTIONSIZINGTEMPLATE = 30
    WP_SMALLCAPTIONSIZINGTEMPLATE = 31
    WP_FRAMELEFTSIZINGTEMPLATE = 32
    WP_SMALLFRAMELEFTSIZINGTEMPLATE = 33
    WP_FRAMERIGHTSIZINGTEMPLATE = 34
    WP_SMALLFRAMERIGHTSIZINGTEMPLATE = 35
    WP_FRAMEBOTTOMSIZINGTEMPLATE = 36
    WP_SMALLFRAMEBOTTOMSIZINGTEMPLATE = 37
    'Public Enum UxThemeButtonParts
    BP_PUSHBUTTON = 1
    BP_RADIOBUTTON = 2
    BP_CHECKBOX = 3
    BP_GROUPBOX = 4
    BP_USERBUTTON = 5
    'Public Enum UxThemeRebarParts
    RP_GRIPPER = 1
    RP_GRIPPERVERT = 2
    RP_BAND = 3
    RP_CHEVRON = 4
    RP_CHEVRONVERT = 5
    'Public Enum UxThemeToolBarParts
    TP_BUTTON = 1
    TP_DROPDOWNBUTTON = 2
    TP_SPLITBUTTON = 3
    TP_SPLITBUTTONDROPDOWN = 4
    TP_SEPARATOR = 5
    TP_SEPARATORVERT = 6
    'Public Enum UxThemeStatusParts
    SP_PANE = 1
    SP_GRIPPERPANE = 2
    SP_GRIPPER = 3
    'Public Enum UxThemeMenuParts
    MP_MENUITEM = 1
    MP_MENUDROPDOWN = 2
    MP_MENUBARITEM = 3
    MP_MENUBARDROPDOWN = 4
    MP_CHEVRON = 5
    MP_SEPARATOR = 6
    'Public Enum UxThemeLISTVIEWParts
    LVP_LISTITEM = 1
    LVP_LISTGROUP = 2
    LVP_LISTDETAIL = 3
    LVP_LISTSORTEDDETAIL = 4
    LVP_EMPTYTEXT = 5
    'Public Enum UxThemeHEADERParts
    HP_HEADERITEM = 1
    HP_HEADERITEMLEFT = 2
    HP_HEADERITEMRIGHT = 3
    HP_HEADERSORTARROW = 4
    'Public Enum UxThemePROGRESSParts
    PP_BAR = 1
    PP_BARVERT = 2
    PP_CHUNK = 3
    PP_CHUNKVERT = 4
    'Public Enum UsxThemeTABParts
    TABP_TABITEM = 1
    TABP_TABITEMLEFTEDGE = 2
    TABP_TABITEMRIGHTEDGE = 3
    TABP_TABITEMBOTHEDGE = 4
    TABP_TOPTABITEM = 5
    TABP_TOPTABITEMLEFTEDGE = 6
    TABP_TOPTABITEMRIGHTEDGE = 7
    TABP_TOPTABITEMBOTHEDGE = 8
    TABP_PANE = 9
    TABP_BODY = 10
    'Public Enum UxThemeTRACKBARParts
    TKP_TRACK = 1
    TKP_TRACKVERT = 2
    TKP_THUMB = 3
    TKP_THUMBBOTTOM = 4
    TKP_THUMBTOP = 5
    TKP_THUMBVERT = 6
    TKP_THUMBLEFT = 7
    TKP_THUMBRIGHT = 8
    TKP_TICS = 9
    TKP_TICSVERT = 10
    'Public Enum UxThemeTOOLTIPParts
    TTP_STANDARD = 1
    TTP_STANDARDTITLE = 2
    TTP_BALLOON = 3
    TTP_BALLOONTITLE = 4
    TTP_CLOSE = 5
    'Public Enum UxThemeTREEVIEWParts
    TVP_TREEITEM = 1
    TVP_GLYPH = 2
    TVP_BRANCH = 3
    'Public Enum UxThemeSPINParts
    SPNP_UP = 1
    SPNP_DOWN = 2
    SPNP_UPHORZ = 3
    SPNP_DOWNHORZ = 4
    'Public Enum UxThemePageParts
    PGRP_UP = 1
    PGRP_DOWN = 2
    PGRP_UPHORZ = 3
    PGRP_DOWNHORZ = 4
    'Public Enum UxThemeSCROLLBARParts
    SBP_ARROWBTN = 1
    SBP_THUMBBTNHORZ = 2
    SBP_THUMBBTNVERT = 3
    SBP_LOWERTRACKHORZ = 4
    SBP_UPPERTRACKHORZ = 5
    SBP_LOWERTRACKVERT = 6
    SBP_UPPERTRACKVERT = 7
    SBP_GRIPPERHORZ = 8
    SBP_GRIPPERVERT = 9
    SBP_SIZEBOX = 10
    'Public Enum UxThemeEDITParts
    EP_EDITTEXT = 1
    EP_CARET = 2
    'Public Enum UxThemeComboBoxParts
    CP_DROPDOWNBUTTON = 1
    'Public Enum UxThemeCLOCKParts
    CLP_TIME = 1
    'Public Enum UxThemeTRAYNOTIFYParts
    TNP_BACKGROUND = 1
    TNP_ANIMBACKGROUND = 2
    'Public Enum UxThemeTASKBARParts
    TBP_BACKGROUNDBOTTOM = 1
    TBP_BACKGROUNDRIGHT = 2
    TBP_BACKGROUNDTOP = 3
    TBP_BACKGROUNDLEFT = 4
    TBP_SIZINGBARBOTTOM = 5
    TBP_SIZINGBARRIGHT = 6
    TBP_SIZINGBARTOP = 7
    TBP_SIZINGBARLEFT = 8
    'Public Enum UxThemeTASKBANDParts
    TDP_GROUPCOUNT = 1
    TDP_FLASHBUTTON = 2
    TDP_FLASHBUTTONGROUPMENU = 3
    'Public Enum UxThemeSTARTPANELParts
    SPP_USERPANE = 1
    SPP_MOREPROGRAMS = 2
    SPP_MOREPROGRAMSARROW = 3
    SPP_PROGLIST = 4
    SPP_PROGLISTSEPARATOR = 5
    SPP_PLACESLIST = 6
    SPP_PLACESLISTSEPARATOR = 7
    SPP_LOGOFF = 8
    SPP_LOGOFFBUTTONS = 9
    SPP_USERPICTURE = 10
    SPP_PREVIEW = 11
    'Public Enum UxThemeEXPLORERBARParts
    EBP_HEADERBACKGROUND = 1
    EBP_HEADERCLOSE = 2
    EBP_HEADERPIN = 3
    EBP_IEBARMENU = 4
    EBP_NORMALGROUPBACKGROUND = 5
    EBP_NORMALGROUPCOLLAPSE = 6
    EBP_NORMALGROUPEXPAND = 7
    EBP_NORMALGROUPHEAD = 8
    EBP_SPECIALGROUPBACKGROUND = 9
    EBP_SPECIALGROUPCOLLAPSE = 10
    EBP_SPECIALGROUPEXPAND = 11
    EBP_SPECIALGROUPHEAD = 12
    'Public Enum UxThemeMENUBANDParts
    MDP_NEWAPPBUTTON = 1
    MDP_SEPERATOR = 2
    'Public Enum UxThemeGLOBALSParts
    GP_BORDER = 1
    GP_LINEHORZ = 2
    GP_LINEVERT = 3
    End Enum
    Public Enum UX_ThemeState As Integer
    DEF_Normal = 1
    '' //---------------------------------------------------------------------------------------
    '' //   "Window" (i.e., non-client) Parts & States
    'Public Enum UxThemeCaptionStates
    CS_ACTIVE = 1
    CS_INACTIVE = 2
    CS_DISABLED = 3
    'Public Enum UxThemeMinCaptionStates
    MNCS_ACTIVE = 1
    MNCS_INACTIVE = 2
    MNCS_DISABLED = 3
    'Public Enum UxThemeMaxCaptionStates
    MXCS_ACTIVE = 1
    MXCS_INACTIVE = 2
    MXCS_DISABLED = 3
    'Public Enum UxThemeFrameStates
    FS_ACTIVE = 1
    FS_INACTIVE = 2
    'Public Enum UxThemeSysButtonStates
    SBS_NORMAL = 1
    SBS_HOT = 2
    SBS_PUSHED = 3
    SBS_DISABLED = 4
    'Public Enum UxThemeMinButtonStates
    MINBS_NORMAL = 1
    MINBS_HOT = 2
    MINBS_PUSHED = 3
    MINBS_DISABLED = 4
    'Public Enum UxThemeMaxButtonStates
    MAXBS_NORMAL = 1
    MAXBS_HOT = 2
    MAXBS_PUSHED = 3
    MAXBS_DISABLED = 4
    'Public Enum UxThemeCloseButtonStates
    CBS_NORMAL = 1
    CBS_HOT = 2
    CBS_PUSHED = 3
    CBS_DISABLED = 4
    'Public Enum UxThemeRestoreButtonStates
    RBS_NORMAL = 1
    RBS_HOT = 2
    RBS_PUSHED = 3
    RBS_DISABLED = 4
    'Public Enum UxThemeHelpButtonStates
    HBS_NORMAL = 1
    HBS_HOT = 2
    HBS_PUSHED = 3
    HBS_DISABLED = 4
    'Public Enum UxThemeHorzScrollStates
    HSS_NORMAL = 1
    HSS_HOT = 2
    HSS_PUSHED = 3
    HSS_DISABLED = 4
    'Public Enum UxThemeHorzThumbStates
    HTS_NORMAL = 1
    HTS_HOT = 2
    HTS_PUSHED = 3
    HTS_DISABLED = 4
    'Public Enum UxThemeVertScrollStates
    VSS_NORMAL = 1
    VSS_HOT = 2
    VSS_PUSHED = 3
    VSS_DISABLED = 4
    'Public Enum UxThemeVertThumbStates
    VTS_NORMAL = 1
    VTS_HOT = 2
    VTS_PUSHED = 3
    VTS_DISABLED = 4
    '' //---------------------------------------------------------------------------------------
    '' //   "Button" Parts & States
    'Public Enum UxThemePushButtonStates
    PBS_NORMAL = 1
    PBS_HOT = 2
    PBS_PRESSED = 3
    PBS_DISABLED = 4
    PBS_DEFAULTED = 5
    'Public Enum UxThemeRadioButtonStates
    RBS_UNCHECKEDNORMAL = 1
    RBS_UNCHECKEDHOT = 2
    RBS_UNCHECKEDPRESSED = 3
    RBS_UNCHECKEDDISABLED = 4
    RBS_CHECKEDNORMAL = 5
    RBS_CHECKEDHOT = 6
    RBS_CHECKEDPRESSED = 7
    RBS_CHECKEDDISABLED = 8
    'Public Enum UxThemeCheckBoxStates
    CBS_UNCHECKEDNORMAL = 1
    CBS_UNCHECKEDHOT = 2
    CBS_UNCHECKEDPRESSED = 3
    CBS_UNCHECKEDDISABLED = 4
    CBS_CHECKEDNORMAL = 5
    CBS_CHECKEDHOT = 6
    CBS_CHECKEDPRESSED = 7
    CBS_CHECKEDDISABLED = 8
    CBS_MIXEDNORMAL = 9
    CBS_MIXEDHOT = 10
    CBS_MIXEDPRESSED = 11
    CBS_MIXEDDISABLED = 12
    'Public Enum UxThemeGroupBoxStates
    GBS_NORMAL = 1
    GBS_DISABLED = 2
    '' //---------------------------------------------------------------------------------------
    '' //   "Rebar" Parts & States
    'Public Enum UxThemeChevronStates
    CHEVS_NORMAL = 1
    CHEVS_HOT = 2
    CHEVS_PRESSED = 3
    '' //---------------------------------------------------------------------------------------
    '' //   "Toolbar" Parts & States
    'Public Enum UxThemeToolBarStates
    TS_NORMAL = 1
    TS_HOT = 2
    TS_PRESSED = 3
    TS_DISABLED = 4
    TS_CHECKED = 5
    TS_HOTCHECKED = 6
    '' //---------------------------------------------------------------------------------------
    '' //   "Status" Parts & States
    '' //---------------------------------------------------------------------------------------
    '' //   "Menu" Parts & States
    'Public Enum UxThemeMenuStates
    MS_NORMAL = 1
    MS_SELECTED = 2
    MS_DEMOTED = 3
    ' //---------------------------------------------------------------------------------------
    ' //   "ListView" Parts & States
    'Public Enum UxThemeLISTITEMStates
    LIS_NORMAL = 1
    LIS_HOT = 2
    LIS_SELECTED = 3
    LIS_DISABLED = 4
    LIS_SELECTEDNOTFOCUS = 5
    ' //---------------------------------------------------------------------------------------
    ' //   "Header" Parts & States
    'Public Enum UxThemeHEADERITEMStates
    HIS_NORMAL = 1
    HIS_HOT = 2
    HIS_PRESSED = 3
    'Public Enum UxThemeHEADERITEMLEFTStates
    HILS_NORMAL = 1
    HILS_HOT = 2
    HILS_PRESSED = 3
    'Public Enum UxThemeHEADERITEMRIGHTStates
    HIRS_NORMAL = 1
    HIRS_HOT = 2
    HIRS_PRESSED = 3
    'Public Enum UxThemeHEADERSORTARROWStates
    HSAS_SORTEDUP = 1
    HSAS_SORTEDDOWN = 2
    ' //---------------------------------------------------------------------------------------
    ' //   "Progress" Parts & States
    ' //---------------------------------------------------------------------------------------
    ' //   "Tab" Parts & States
    'Public Enum UxThemeTABITEMStates
    TIS_NORMAL = 1
    TIS_HOT = 2
    TIS_SELECTED = 3
    TIS_DISABLED = 4
    TIS_FOCUSED = 5
    'Public Enum UxThemeTABITEMLEFTEDGEStates
    TILES_NORMAL = 1
    TILES_HOT = 2
    TILES_SELECTED = 3
    TILES_DISABLED = 4
    TILES_FOCUSED = 5
    'Public Enum UxThemeTABITEMRIGHTEDGEStates
    TIRES_NORMAL = 1
    TIRES_HOT = 2
    TIRES_SELECTED = 3
    TIRES_DISABLED = 4
    TIRES_FOCUSED = 5
    'Public Enum UxThemeTABITEMBOTHEDGESStates
    TIBES_NORMAL = 1
    TIBES_HOT = 2
    TIBES_SELECTED = 3
    TIBES_DISABLED = 4
    TIBES_FOCUSED = 5
    'Public Enum UxThemeTOPTABITEMStates
    TTIS_NORMAL = 1
    TTIS_HOT = 2
    TTIS_SELECTED = 3
    TTIS_DISABLED = 4
    TTIS_FOCUSED = 5
    'Public Enum UxThemeTOPTABITEMLEFTEDGEStates
    TTILES_NORMAL = 1
    TTILES_HOT = 2
    TTILES_SELECTED = 3
    TTILES_DISABLED = 4
    TTILES_FOCUSED = 5
    'Public Enum UxThemeTOPTABITEMRIGHTEDGEStates
    TTIRES_NORMAL = 1
    TTIRES_HOT = 2
    TTIRES_SELECTED = 3
    TTIRES_DISABLED = 4
    TTIRES_FOCUSED = 5
    'Public Enum UxThemeTOPTABITEMBOTHEDGESStates
    TTIBES_NORMAL = 1
    TTIBES_HOT = 2
    TTIBES_SELECTED = 3
    TTIBES_DISABLED = 4
    TTIBES_FOCUSED = 5
    ' //---------------------------------------------------------------------------------------
    ' //   "Trackbar" Parts & States
    'Public Enum UxThemeTRACKBARStates
    TKS_NORMAL = 1
    'Public Enum UxThemeTRACKStates
    TRS_NORMAL = 1
    'Public Enum UxThemeTRACKVERTStates
    TRVS_NORMAL = 1
    'Public Enum UxThemeTHUMBStates
    TUS_NORMAL = 1
    TUS_HOT = 2
    TUS_PRESSED = 3
    TUS_FOCUSED = 4
    TUS_DISABLED = 5
    'Public Enum UxThemeTHUMBBOTTOMStates
    TUBS_NORMAL = 1
    TUBS_HOT = 2
    TUBS_PRESSED = 3
    TUBS_FOCUSED = 4
    TUBS_DISABLED = 5
    'Public Enum UxThemeTHUMBTOPStates
    TUTS_NORMAL = 1
    TUTS_HOT = 2
    TUTS_PRESSED = 3
    TUTS_FOCUSED = 4
    TUTS_DISABLED = 5
    'Public Enum UxThemeTHUMBVERTStates
    TUVS_NORMAL = 1
    TUVS_HOT = 2
    TUVS_PRESSED = 3
    TUVS_FOCUSED = 4
    TUVS_DISABLED = 5
    'Public Enum UxThemeTHUMBLEFTStates
    TUVLS_NORMAL = 1
    TUVLS_HOT = 2
    TUVLS_PRESSED = 3
    TUVLS_FOCUSED = 4
    TUVLS_DISABLED = 5
    'Public Enum UxThemeTHUMBRIGHTStates
    TUVRS_NORMAL = 1
    TUVRS_HOT = 2
    TUVRS_PRESSED = 3
    TUVRS_FOCUSED = 4
    TUVRS_DISABLED = 5
    'Public Enum UxThemeTICSStates
    TSS_NORMAL = 1
    'Public Enum UxThemeTICSVERTStates
    TSVS_NORMAL = 1
    ' //---------------------------------------------------------------------------------------
    ' //   "Tooltips" Parts & States
    'Public Enum UxThemeCLOSEStates
    TTCS_NORMAL = 1
    TTCS_HOT = 2
    TTCS_PRESSED = 3
    'Public Enum UxThemeSTANDARDStates
    TTSS_NORMAL = 1
    TTSS_LINK = 2
    'Public Enum UxThemeBALLOONStates
    TTBS_NORMAL = 1
    TTBS_LINK = 2
    ' //---------------------------------------------------------------------------------------
    ' //   "TreeView" Parts & States
    'Public Enum UxThemeTREEITEMStates
    TREIS_NORMAL = 1
    TREIS_HOT = 2
    TREIS_SELECTED = 3
    TREIS_DISABLED = 4
    TREIS_SELECTEDNOTFOCUS = 5
    'Public Enum UxThemeGLYPHStates
    GLPS_CLOSED = 1
    GLPS_OPENED = 2
    ' //---------------------------------------------------------------------------------------
    ' //   "Spin" Parts & States
    'Public Enum UxThemeSPINUPStates
    UPS_NORMAL = 1
    UPS_HOT = 2
    UPS_PRESSED = 3
    UPS_DISABLED = 4
    'Public Enum UxThemeSPINDOWNStates
    DNS_NORMAL = 1
    DNS_HOT = 2
    DNS_PRESSED = 3
    DNS_DISABLED = 4
    'Public Enum UxThemeSPINUPHORZStates
    UPHZS_NORMAL = 1
    UPHZS_HOT = 2
    UPHZS_PRESSED = 3
    UPHZS_DISABLED = 4
    'Public Enum UxThemeSPINDOWNHORZStates
    DNHZS_NORMAL = 1
    DNHZS_HOT = 2
    DNHZS_PRESSED = 3
    DNHZS_DISABLED = 4
    ' //---------------------------------------------------------------------------------------
    ' //   "Page" Parts & States
    'Public Enum UxThemePAGEUPStates
    ' //---------------------------------------------------------------------------------------
    ' //   "Scrollbar" Parts & States
    'Public Enum UxThemeARROWBTNStates
    ABS_UPNORMAL = 1
    ABS_UPHOT = 2
    ABS_UPPRESSED = 3
    ABS_UPDISABLED = 4
    ABS_DOWNNORMAL = 5
    ABS_DOWNHOT = 6
    ABS_DOWNPRESSED = 7
    ABS_DOWNDISABLED = 8
    ABS_LEFTNORMAL = 9
    ABS_LEFTHOT = 10
    ABS_LEFTPRESSED = 11
    ABS_LEFTDISABLED = 12
    ABS_RIGHTNORMAL = 13
    ABS_RIGHTHOT = 14
    ABS_RIGHTPRESSED = 15
    ABS_RIGHTDISABLED = 16
    'Public Enum UxThemeSCROLLBARStates
    SCRBS_NORMAL = 1
    SCRBS_HOT = 2
    SCRBS_PRESSED = 3
    SCRBS_DISABLED = 4
    'Public Enum UxThemeSIZEBOXStates
    SZB_RIGHTALIGN = 1
    SZB_LEFTALIGN = 2
    ' //---------------------------------------------------------------------------------------
    ' //   "Edit" Parts & States
    'Public Enum UxThemeEDITTEXTStates
    ETS_NORMAL = 1
    ETS_HOT = 2
    ETS_SELECTED = 3
    ETS_DISABLED = 4
    ETS_FOCUSED = 5
    ETS_READONLY = 6
    ETS_ASSIST = 7
    ' //---------------------------------------------------------------------------------------
    ' //   "ComboBox" Parts & States
    'Public Enum UxThemeComboBoxStates
    CBXS_NORMAL = 1
    CBXS_HOT = 2
    CBXS_PRESSED = 3
    CBXS_DISABLED = 4
    ' //---------------------------------------------------------------------------------------
    ' //   "Taskbar Clock" Parts & States
    'Public Enum UxThemeCLOCKStates
    CLS_NORMAL = 1
    ' //---------------------------------------------------------------------------------------
    ' //   "Tray Notify" Parts & States
    ' //---------------------------------------------------------------------------------------
    ' //   "TaskBar" Parts & States
    ' //---------------------------------------------------------------------------------------
    ' //   "TaskBand" Parts & States
    ' //---------------------------------------------------------------------------------------
    ' //   "StartPanel" Parts & States
    'Public Enum UxThemeMOREPROGRAMSARROWStates
    SPS_NORMAL = 1
    SPS_HOT = 2
    SPS_PRESSED = 3
    'Public Enum UxThemeLOGOFFBUTTONSStates
    SPLS_NORMAL = 1
    SPLS_HOT = 2
    SPLS_PRESSED = 3
    ' //---------------------------------------------------------------------------------------
    ' //   "ExplorerBar" Parts & States
    'Public Enum UxThemeHEADERCLOSEStates
    EBHC_NORMAL = 1
    EBHC_HOT = 2
    EBHC_PRESSED = 3
    'Public Enum UxThemeHEADERPINStates
    EBHP_NORMAL = 1
    EBHP_HOT = 2
    EBHP_PRESSED = 3
    EBHP_SELECTEDNORMAL = 4
    EBHP_SELECTEDHOT = 5
    EBHP_SELECTEDPRESSED = 6
    'Public Enum UxThemeIEBARMENUStates
    EBM_NORMAL = 1
    EBM_HOT = 2
    EBM_PRESSED = 3
    'Public Enum UxThemeNORMALGROUPCOLLAPSEStates
    EBNGC_NORMAL = 1
    EBNGC_HOT = 2
    EBNGC_PRESSED = 3
    'Public Enum UxThemeNORMALGROUPEXPANDStates
    EBNGE_NORMAL = 1
    EBNGE_HOT = 2
    EBNGE_PRESSED = 3
    'Public Enum UxThemeSPECIALGROUPCOLLAPSEStates
    EBSGC_NORMAL = 1
    EBSGC_HOT = 2
    EBSGC_PRESSED = 3
    'Public Enum UxThemeSPECIALGROUPEXPANDStates
    EBSGE_NORMAL = 1
    EBSGE_HOT = 2
    EBSGE_PRESSED = 3
    ' //---------------------------------------------------------------------------------------
    ' //   "TaskBand" Parts & States
    'Public Enum UxThemeMENUBANDStates
    MDS_NORMAL = 1
    MDS_HOT = 2
    MDS_PRESSED = 3
    MDS_DISABLED = 4
    MDS_CHECKED = 5
    MDS_HOTCHECKED = 6
    ' //---------------------------------------------------------------------------------------
    ' //   "Globals" Parts & States
    'Public Enum UxThemeGLOBALSBORDERStates
    BSS_FLAT = 1
    BSS_RAISED = 2
    BSS_SUNKEN = 3
    'Public Enum UxThemeGLOBALSBORDERStates
    LHS_FLAT = 1
    LHS_RAISED = 2
    LHS_SUNKEN = 3
    'Public Enum UxThemeGLOBALSBORDERStates
    LVS_FLAT = 1
    LVS_RAISED = 2
    LVS_SUNKEN = 3
    End Enum

    <DllImport("UxTheme.dll", ExactSpelling:=True, CallingConvention:=CallingConvention.Cdecl, CharSet:=CharSet.Unicode)> _
    Public Overloads Shared Function IsAppThemed() As Boolean
    End Function
    ' IsAppThemed will return true if the Os is themed even if the app is not.
    ' To overcome this problem we must also check which version of ComCtl32.dll is
    ' being used. Since ComCtl32.dll version 6 is exclusive to WindowsXP, we do not 
    ' need to check the OSVersion.
    Public ReadOnly Property IsAppXPThemed() As Boolean
    Get
        Dim dllVer As New DLLVERSIONINFO
        dllVer.cbSize = Marshal.SizeOf(dllVer)
        DllGetVersion(dllVer)
        If dllVer.dwMajorVersion >= 6 Then If IsAppThemed() Then Return True
    End Get
    End Property
    '//
```

## Sample Code:
```cs
'// Use the P/Invoke API
     Public Function DrawThemedText(ByVal Text As String, ByVal ThemeClass As UX_ThemeClass, ByVal ThemePart As UX_ThemePart, ByVal ThemeState As UX_ThemeState, ByVal Bounds As Rectangle) As Bitmap
    ' The handle for the theme objects.
    Dim My_ThemeHandle As IntPtr
    ' Setup String Pointer.
    Dim My_ThemeText As String = Text
    ' Create Destination Bitmap from bounding dimensions.
    Dim My_Bitmap As New Bitmap(Bounds.Width, Bounds.Height)
    ' Create Graphics to ge the HDC from.
    Dim My_Graphics As Graphics = Graphics.FromImage(My_Bitmap)
    ' If Themed then draw themed, otherwise draw non-themed.
    If IsAppXPThemed Then
        ' Get the HDC from the hidden atribute.
        Dim My_HDC As IntPtr = My_Graphics.GetHdc
        ' If we have a Pointer open we will now close it.
        If Not My_ThemeHandle.Equals(IntPtr.Zero) Then CloseThemeData(My_ThemeHandle)
        ' We will now open a pointer to a Theme Data object. Notice that the string is being parsed from the Enum.
        My_ThemeHandle = OpenThemeData(Me.Handle, [Enum].GetName(GetType(UX_ThemeClass), ThemeClass))
        If My_ThemeText.Text <> "" Then
        ' Draw Theme Background to the destination Bitmap.
        DrawThemeText(My_ThemeHandle, My_HDC, ThemePart, ThemeState, My_ThemeText, -1, DrawTextFlags.DT_CENTER Or DrawTextFlags.DT_VCENTER, 0, Bounds)
        End If
        ' HDC is do longer required so clean it up.
        My_Graphics.ReleaseHdc(My_HDC)
    End If
    ' Finished using the Graphics object so dispose of it.
    My_Graphics.Dispose()
    ' Return the extracted bitmap.
    Return My_Bitmap
    End Function
    '//

    '// How to use the Functions
    Private Sub Form1_Paint(ByVal sender As Object, ByVal e As System.Windows.Forms.PaintEventArgs) Handles MyBase.Paint
    e.Graphics.DrawImage(DrawThemedText("Hellow World!", UX_ThemeClass.Button, UX_ThemePart.BP_PUSHBUTTON, UX_ThemeState.ABS_DOWNHOT, New Rectangle(Point.Empty, Me.Size)), Point.Empty)
    End Sub
    '//
```
