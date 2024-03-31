
## C# Definition:
```cs
[ComImport]
    [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    [Guid("79D16DE4-ABEE-4021-8D9D-9169B261D657")]
    public interface IDeskBand2
    {
        // IOleWindow methods
        [PreserveSig]
        int GetWindow(out IntPtr phwnd);
        [PreserveSig]
        int ContextSensitiveHelp([In, MarshalAs(UnmanagedType.Bool)] bool fEnterMode);

        // IDockingWindow methods
        [PreserveSig]
        int ShowDW([In, MarshalAs(UnmanagedType.Bool)] bool fShow);
        [PreserveSig]
        int CloseDW([In] Int32 dwReserved);
        [PreserveSig]
        int ResizeBorderDW(ref RECT rcBorder, [In, MarshalAs(UnmanagedType.IUnknown)] ref object punkToolbarSite, [MarshalAs(UnmanagedType.Bool)] bool fReserved);

        // IDeskBand methods
        [PreserveSig]
        int GetBandInfo([In] Int32 dwBandID, [In] Int32 dwViewMode, [In, Out] ref DESKBANDINFO pdbi);

        // IDeskband2 methods
        void CanRenderComposited(out bool pfCanRenderComposited);
        void SetCompositionState(bool fCompositionEnabled);
        void GetCompositionState(out bool pfCompositionEnabled);
    }
```

## VB Definition:
```cs
<ComImport()> _
```

## VB Definition:
```cs
Sub GetBandInfo(dwBandID As UInt32, dwViewMode As UInt32, ByRef pdbi As DESKBANDINFO)
    Sub CanRenderComposited(ByRef pfCanRenderComposited As Boolean)
    Sub GetCompositionState(ByRef pfCompositionEnabled As Boolean)
    Sub SetCompositionState(<MarshalAs(UnmanagedType.Bool)> fCompositionEnabled As Boolean)
```

## VB Sample
```cs
Inherits UserControl
    Implements IObjectWithSite
    ' Implements IDeskBand
    Implements IDeskBand
    Implements IDockingWindow
    Implements IOleWindow
    Implements IInputObject
    Implements IDeskBand2
    ''' <summary>
    ''' Reference to the host explorer.
    ''' </summary>
    Protected Explorer As WebBrowserClass
    Protected BandObjectSite As IInputObjectSite
    ''' <summary>
    ''' This event is fired after reference to hosting explorer is retreived and stored in Explorer property.
    ''' </summary>
    Public Event ExplorerAttached As EventHandler

    Public Sub New()
    InitializeComponent()
    End Sub

    Private Sub InitializeComponent()
    Me.SuspendLayout()
    '
    'BandObject
    '
    Me.BackColor = System.Drawing.Color.Transparent
    Me.Name = "BandObject"
    Me.ResumeLayout(False)

    End Sub

    ' Function ShowDeskBand(<[In](), MarshalAs(UnmanagedType.Struct)> ByRef clsid As Guid) As Integer Implements IDeskBand2.ShowDeskBand

    ' End Function

    ' Function HideDeskBand(<[In](), MarshalAs(UnmanagedType.Struct)> ByRef clsid As Guid) As Integer Implements IDeskBand.HideDeskBand

    ' End Function
    ' Function IsDeskBandShown(<[In](), MarshalAs(UnmanagedType.Struct)> ByRef clsid As Guid) As Integer Implements IDeskBand2.IsDeskBandShown

    'End Function
    ' Function DeskBandRegistrationChanged() As Integer Implements IDeskBand2.DeskBandRegistrationChanged

    ' End Function

    ''' <summary>
    ''' Title of band object. Displayed at the left or on top of the band object.
    ''' </summary>
    <Browsable(True)> _
    <DefaultValue("")> _
    Public Property Title() As [String]
    Get
        Return _title
    End Get
    Set(value As [String])
        _title = value
    End Set
    End Property
    Private _title As [String]
```

## VB Sample
```cs
''' <summary>
    ''' Minimum size of the band object. Default value of -1 sets no minimum constraint.
    ''' </summary>
    <Browsable(True)> _
    <DefaultValue(GetType(Size), "-1,-1")> _
    Public Property MinSize() As Size
    Get
        Return _minSize
    End Get
    Set(value As Size)
        _minSize = value
    End Set
    End Property
    Private _minSize As New Size(-1, -1)

    ''' <summary>
    ''' Maximum size of the band object. Default value of -1 sets no maximum constraint.
    ''' </summary>
    <Browsable(True)> _
    <DefaultValue(GetType(Size), "-1,-1")> _
    Public Property MaxSize() As Size
    Get
        Return _maxSize
    End Get
    Set(value As Size)
        _maxSize = value
    End Set
    End Property
    Private _maxSize As New Size(-1, -1)

    ''' <summary>
    ''' Says that band object's size must be multiple of this size. Defauilt value of -1 does not set this constraint.
    ''' </summary>
    <Browsable(True)> _
    <DefaultValue(GetType(Size), "-1,-1")> _
    Public Property IntegralSize() As Size
    Get
        Return _integralSize
    End Get
    Set(value As Size)
        _integralSize = value
    End Set
    End Property
    Private _integralSize As New Size(-1, -1)
```

## VB Sample
```cs
Public Overridable Sub GetBandInfo(dwBandID As UInt32, dwViewMode As UInt32, ByRef dbi As DESKBANDINFO) Implements IDeskBand.GetBandInfo, IDeskBand2.GetBandInfo
    dbi.wszTitle = Me.Title

    dbi.ptActual.x = Me.Size.Width
    dbi.ptActual.y = Me.Size.Height

    dbi.ptMaxSize.x = Me.MaxSize.Width
    dbi.ptMaxSize.y = Me.MaxSize.Height

    dbi.ptMinSize.x = Me.MinSize.Width
    dbi.ptMinSize.y = Me.MinSize.Height

    dbi.ptIntegral.x = Me.IntegralSize.Width
    dbi.ptIntegral.y = Me.IntegralSize.Height

    dbi.dwModeFlags = DBIM.TITLE Or DBIM.ACTUAL Or DBIM.MAXSIZE Or DBIM.MINSIZE Or DBIM.INTEGRAL
    End Sub
    Sub CanRenderComposited(ByRef pfCanRenderComposited As Boolean) Implements IDeskBand2.CanRenderComposited
    pfCanRenderComposited = True

    End Sub
    Sub GetCompositionState(ByRef pfCompositionEnabled As Boolean) Implements IDeskBand2.GetCompositionState

    pfCompositionEnabled = True
    End Sub
    Sub SetCompositionState(<MarshalAs(UnmanagedType.Bool)> fCompositionEnabled As Boolean) Implements IDeskBand2.SetCompositionState
    fCompositionEnabled = True

    End Sub
    ''' <summary>
    ''' Called by explorer when band object needs to be showed or hidden.
    ''' </summary>
    ''' <param name="fShow"></param>
    Public Overridable Sub ShowDW(fShow As Boolean) Implements IDeskBand.ShowDW, IDockingWindow.ShowDW
    If fShow Then
        Show()
    Else
        Hide()
    End If
    End Sub

    ''' <summary>
    ''' Called by explorer when window is about to close.
    ''' </summary>
    Public Overridable Sub CloseDW(dwReserved As UInt32) Implements IDeskBand.CloseDW, IDockingWindow.CloseDW
    Dispose(True)
    End Sub

    ''' <summary>
    ''' Not used.
    ''' </summary>
    Public Overridable Sub ResizeBorderDW(prcBorder As IntPtr, punkToolbarSite As [Object], fReserved As Boolean) Implements IDeskBand.ResizeBorderDW, IDockingWindow.ResizeBorderDW
    End Sub

    Public Overridable Sub GetWindow(ByRef phwnd As System.IntPtr) Implements IDeskBand.GetWindow, IDockingWindow.GetWindow, IOleWindow.GetWindow
    phwnd = Handle
    End Sub

    Public Overridable Sub ContextSensitiveHelp(fEnterMode As Boolean) Implements IDeskBand.ContextSensitiveHelp, IDockingWindow.ContextSensitiveHelp, IOleWindow.ContextSensitiveHelp
    End Sub

    Public Overridable Sub SetSite(pUnkSite As [Object]) Implements IObjectWithSite.SetSite
    If BandObjectSite IsNot Nothing Then
        Marshal.ReleaseComObject(BandObjectSite)
    End If

    If Explorer IsNot Nothing Then
        Marshal.ReleaseComObject(Explorer)
        Explorer = Nothing
    End If

    BandObjectSite = DirectCast(pUnkSite, IInputObjectSite)
    If BandObjectSite IsNot Nothing Then
        'pUnkSite is a pointer to object that implements IOleWindowSite or something  similar
        'we need to get access to the top level object - explorer itself
        'to allows this explorer objects also implement IServiceProvider interface
        '(don't mix it with System.IServiceProvider!)
        'we get this interface and ask it to find WebBrowserApp
        Dim sp As _IServiceProvider = TryCast(BandObjectSite, _IServiceProvider)
        Dim guid As Guid = ExplorerGUIDs.IID_IWebBrowserApp
        Dim riid As Guid = ExplorerGUIDs.IID_IUnknown

        Try
        Dim w As Object
        sp.QueryService(guid, riid, w)

        'once we have interface to the COM object we can create RCW from it
        Explorer = DirectCast(Marshal.CreateWrapperOfType(TryCast(w, IWebBrowser), GetType(WebBrowserClass)), WebBrowserClass)

        OnExplorerAttached(EventArgs.Empty)
        'we anticipate this exception in case our object instantiated 
        'as a Desk Band. There is no web browser service available.
        Catch generatedExceptionName As COMException
        End Try
    End If

    End Sub

    Public Overridable Sub GetSite(ByRef riid As Guid, ByRef ppvSite As [Object]) Implements IObjectWithSite.GetSite
    ppvSite = BandObjectSite
    End Sub

    ''' <summary>
    ''' Called explorer when focus has to be chenged.
    ''' </summary>
    Public Overridable Sub UIActivateIO(fActivate As Int32, ByRef Msg As MSG) Implements IInputObject.UIActivateIO
    If fActivate <> 0 Then
        Dim ctrl As Control = GetNextControl(Me, True)
        'first
        If ModifierKeys = Keys.Shift Then
        ctrl = GetNextControl(ctrl, False)
        End If
        'last
        If ctrl IsNot Nothing Then
        ctrl.[Select]()
        End If
        Me.Focus()
    End If
    End Sub

    Public Overridable Function HasFocusIO() As Int32 Implements IInputObject.HasFocusIO
    Return If(Me.ContainsFocus, 0, 1)
    'S_OK : S_FALSE;
    End Function

    ''' <summary>
    ''' Called by explorer to process keyboard events. Undersatands Tab and F6.
    ''' </summary>
    ''' <param name="msg"></param>
    ''' <returns>S_OK if message was processed, S_FALSE otherwise.</returns>
    Public Overridable Function TranslateAcceleratorIO(ByRef msg As MSG) As Int32 Implements IInputObject.TranslateAcceleratorIO
    If msg.message = &H100 Then
        'WM_KEYDOWN
        If msg.wParam = CUInt(Keys.Tab) OrElse msg.wParam = CUInt(Keys.F6) Then
        'keys used by explorer to navigate from control to control
        If SelectNextControl(ActiveControl, If(ModifierKeys = Keys.Shift, False, True), True, True, False) Then
            Return 0
        End If
        End If
    End If
    'S_OK
    Return 1
    'S_FALSE
    End Function

    ''' <summary>
    ''' Override this method to handle ExplorerAttached event.
    ''' </summary>
    ''' <param name="ea"></param>
    Protected Overridable Sub OnExplorerAttached(ea As EventArgs)
    RaiseEvent ExplorerAttached(Me, ea)
    End Sub

    ''' <summary>
    ''' Notifies explorer of focus change.
    ''' </summary>
    Protected Overrides Sub OnGotFocus(e As System.EventArgs)
    MyBase.OnGotFocus(e)
    BandObjectSite.OnFocusChangeIS(TryCast(Me, IInputObject), 1)
    End Sub
    ''' <summary>
    ''' Notifies explorer of focus change.
    ''' </summary>
    Protected Overrides Sub OnLostFocus(e As System.EventArgs)
    MyBase.OnLostFocus(e)
    If ActiveControl Is Nothing Then
        BandObjectSite.OnFocusChangeIS(TryCast(Me, IInputObject), 0)
    End If
    End Sub
```

## VB Sample
```cs
''' <summary>
    ''' Called when derived class is registered as a COM server.
    ''' </summary>
    <ComRegisterFunctionAttribute()> _
    Public Shared Sub Register(t As Type)
    Dim guid As String = t.GUID.ToString("B")

    Dim rkClass As RegistryKey = Registry.ClassesRoot.CreateSubKey("CLSID\" & guid)
    Dim rkCat As RegistryKey = rkClass.CreateSubKey("Implemented Categories")

    Dim boa As BandObjectAttribute() = DirectCast(t.GetCustomAttributes(GetType(BandObjectAttribute), False), BandObjectAttribute())

    Dim name As String = t.Name
    Dim help As String = t.Name
    Dim style As BandObjectStyle = 0
    If boa.Length = 1 Then
        If boa(0).Name IsNot Nothing Then
        name = boa(0).Name
        End If

        If boa(0).HelpText IsNot Nothing Then
        help = boa(0).HelpText
        End If

        style = boa(0).Style
    End If

    rkClass.SetValue(Nothing, name)
    rkClass.SetValue("MenuText", name)
    rkClass.SetValue("HelpText", help)

    If 0 <> (style And BandObjectStyle.Vertical) Then
        rkCat.CreateSubKey("{00021493-0000-0000-C000-000000000046}")
    End If

    If 0 <> (style And BandObjectStyle.Horizontal) Then
        rkCat.CreateSubKey("{00021494-0000-0000-C000-000000000046}")
    End If

    If 0 <> (style And BandObjectStyle.TaskbarToolBar) Then
        rkCat.CreateSubKey("{0DF44EAA-FF21-4412-828E-260A8728E7F1}")
    End If

    If 0 <> (style And BandObjectStyle.ExplorerToolbar) Then
        Registry.LocalMachine.CreateSubKey("SOFTWARE\Microsoft\Internet Explorer\Toolbar").SetValue(guid, name)
    End If

    End Sub

    ''' <summary>
    ''' Called when derived class is unregistered as a COM server.
    ''' </summary>
    <ComUnregisterFunctionAttribute()> _
    Public Shared Sub Unregister(t As Type)
    Dim guid As String = t.GUID.ToString("B")
    Dim boa As BandObjectAttribute() = DirectCast(t.GetCustomAttributes(GetType(BandObjectAttribute), False), BandObjectAttribute())

    Dim style As BandObjectStyle = 0
    If boa.Length = 1 Then
        style = boa(0).Style
    End If

    If 0 <> (style And BandObjectStyle.ExplorerToolbar) Then
        Registry.LocalMachine.CreateSubKey("SOFTWARE\Microsoft\Internet Explorer\Toolbar").DeleteValue(guid, False)
    End If

    Registry.ClassesRoot.CreateSubKey("CLSID").DeleteSubKeyTree(guid)
    End Sub
```

## VB Sample
```cs
Imports System.ComponentModel
    Imports System.Windows.Forms

    Imports BandObjectLib
    Imports System.Runtime.InteropServices

    <Guid("C6FC82EA-AF64-43AF-BA1F-32A634C5FCC7")> _
    <BandObject("Hello World Bar", BandObjectStyle.Horizontal Or BandObjectStyle.TaskbarToolBar, HelpText:="Shows bar that says hello.")> _
```

## VB Sample
```cs
Inherits BandObject
    Private WithEvents button1 As System.Windows.Forms.Button
    Private components As System.ComponentModel.Container = Nothing

    Public Sub New()
        InitializeComponent()
    End Sub

    Protected Overrides Sub Dispose(disposing As Boolean)
        If disposing Then
        If components IsNot Nothing Then
            components.Dispose()
        End If
        End If
        MyBase.Dispose(disposing)
    End Sub
```

## VB Sample
```cs
Private Sub InitializeComponent()
        Me.button1 = New System.Windows.Forms.Button()
        Me.SuspendLayout()
        '
        'button1
        '
        Me.button1.Anchor = CType((((System.Windows.Forms.AnchorStyles.Top Or System.Windows.Forms.AnchorStyles.Bottom) _
        Or System.Windows.Forms.AnchorStyles.Left) _
        Or System.Windows.Forms.AnchorStyles.Right), System.Windows.Forms.AnchorStyles)
        Me.button1.BackColor = System.Drawing.SystemColors.HotTrack
        Me.button1.ForeColor = System.Drawing.SystemColors.Info
        Me.button1.Location = New System.Drawing.Point(0, 0)
        Me.button1.Name = "button1"
        Me.button1.Size = New System.Drawing.Size(62, 24)
        Me.button1.TabIndex = 0
        Me.button1.Text = "Say Hello"
        Me.button1.UseVisualStyleBackColor = False
        '
        'HelloWorldBar2
        '
        Me.Controls.Add(Me.button1)
        Me.MinSize = New System.Drawing.Size(150, 24)
        Me.Name = "HelloWorldBar2"
        Me.Size = New System.Drawing.Size(62, 24)
        Me.Title = "Hello Bar"
        Me.ResumeLayout(False)

    End Sub
```

## VB Sample
```cs
Private Sub button1_Click(sender As Object, e As System.EventArgs) Handles button1.Click
        MessageBox.Show("ZZZZZZ Hello, World!")
    End Sub
    End Class
```

## VB Sample
```cs
ComIntorp:
```

## VB Sample
```cs
Public Shared ReadOnly IID_IWebBrowserApp As New Guid("{0002DF05-0000-0000-C000-000000000046}")
    Public Shared ReadOnly IID_IUnknown As New Guid("{00000000-0000-0000-C000-000000000046}")
```

## VB Sample
```cs
MINSIZE = &H1
    MAXSIZE = &H2
    INTEGRAL = &H4
    ACTUAL = &H8
    TITLE = &H10
    MODEFLAGS = &H20
    BKCOLOR = &H40
```

## VB Sample
```cs
Public dwMask As UInt32
    Public ptMinSize As Point
    Public ptMaxSize As Point
    Public ptIntegral As Point
    Public ptActual As Point
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst := 255)> _
    Public wszTitle As [String]
    Public dwModeFlags As DBIM
    Public crBkgnd As Int32
```

## VB Sample
```cs
Sub SetSite(<[In], MarshalAs(UnmanagedType.IUnknown)> pUnkSite As [Object])
    Sub GetSite(ByRef riid As Guid, <MarshalAs(UnmanagedType.IUnknown)> ByRef ppvSite As [Object])
```

## VB Sample
```cs
<PreserveSig()> _
    Function ShowDeskBand(<[In](), MarshalAs(UnmanagedType.Struct)> ByRef clsid As Guid) As Integer
    <PreserveSig()> _
    Function HideDeskBand(<[In](), MarshalAs(UnmanagedType.Struct)> ByRef clsid As Guid) As Integer
    <PreserveSig()> _
    Function IsDeskBandShown(<[In](), MarshalAs(UnmanagedType.Struct)> ByRef clsid As Guid) As Integer
    <PreserveSig()> _
    Function DeskBandRegistrationChanged() As Integer
```

## VB Sample
```cs
Sub GetWindow(ByRef phwnd As System.IntPtr)
    Sub ContextSensitiveHelp(<[In]> fEnterMode As Boolean)
```

## VB Sample
```cs
Sub GetWindow(ByRef phwnd As System.IntPtr)
    Sub ContextSensitiveHelp(<[In]> fEnterMode As Boolean)

    Sub ShowDW(<[In]> fShow As Boolean)
    Sub CloseDW(<[In]> dwReserved As UInt32)
    Sub ResizeBorderDW(prcBorder As IntPtr, <[In], MarshalAs(UnmanagedType.IUnknown)> punkToolbarSite As [Object], fReserved As Boolean)
```

## VB Sample
```cs
Sub GetBandInfo(dwBandID As UInt32, dwViewMode As UInt32, ByRef pdbi As DESKBANDINFO)
    Sub CanRenderComposited(ByRef pfCanRenderComposited As Boolean)
    Sub GetCompositionState(ByRef pfCompositionEnabled As Boolean)
    Sub SetCompositionState(<MarshalAs(UnmanagedType.Bool)> fCompositionEnabled As Boolean)
```

## VB Sample
```cs
Sub GetWindow(ByRef phwnd As System.IntPtr)
    Sub ContextSensitiveHelp(<[In]()> fEnterMode As Boolean)
    Sub ShowDW(<[In]()> fShow As Boolean)
    Sub CloseDW(<[In]()> dwReserved As UInt32)
    Sub ResizeBorderDW(prcBorder As IntPtr, <[In](), MarshalAs(UnmanagedType.IUnknown)> punkToolbarSite As [Object], fReserved As Boolean)
    Sub GetBandInfo(dwBandID As UInt32, dwViewMode As UInt32, ByRef pdbi As DESKBANDINFO)
```

## VB Sample
```cs
Sub GetClassID(ByRef pClassID As Guid)
```

## VB Sample
```cs
Sub GetClassID(ByRef pClassID As Guid)
    Sub IsDirty()
    Sub Load(<[In], MarshalAs(UnmanagedType.[Interface])> pStm As [Object])
    Sub Save(<[In], MarshalAs(UnmanagedType.[Interface])> pStm As [Object], <[In]> fClearDirty As Boolean)
    Sub GetSizeMax(<Out> ByRef pcbSize As UInt64)
```

## VB Sample
```cs
Sub QueryService(ByRef guid As Guid, ByRef riid As Guid, <MarshalAs(UnmanagedType.[Interface])> ByRef Obj As [Object])
```

## VB Sample
```cs
Sub UIActivateIO(fActivate As Int32, ByRef msg As MSG)

    '[return:MarshalAs(UnmanagedType.Error)]
    <PreserveSig> _
    Function HasFocusIO() As Int32

    <PreserveSig> _
    Function TranslateAcceleratorIO(ByRef msg As MSG) As Int32
```

## VB Sample
```cs
<PreserveSig> _
    Function OnFocusChangeIS(<MarshalAs(UnmanagedType.IUnknown)> punkObj As [Object], fSetFocus As Int32) As Int32
```

## VB Sample
```cs
Public x As Int32
    Public y As Int32
```

## VB Sample
```cs
Public hwnd As IntPtr
    Public message As UInt32
    Public wParam As UInt32
    Public lParam As Int32
    Public time As UInt32
    Public pt As POINT
```

## VB Sample
```cs
Attributes:
```

## VB Sample
```cs
Vertical = 1
    Horizontal = 2
    ExplorerToolbar = 4
    TaskbarToolBar = 8
```

## VB Sample
```cs
Inherits System.Attribute
    Public Sub New()
    End Sub

    Public Sub New(name__1 As String, style__2 As BandObjectStyle)
        Name = name__1
        Style = style__2
    End Sub
    Public Style As BandObjectStyle
    Public Name As String
    Public HelpText As String
```
