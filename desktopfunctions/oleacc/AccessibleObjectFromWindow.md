
## C# Signature:
```cs
[DllImport("oleacc.dll")]
    internal static extern int AccessibleObjectFromWindow(
         IntPtr hwnd, 
         uint id, 
         ref Guid iid, 
         [In, Out, MarshalAs(UnmanagedType.IUnknown)] ref object ppvObject);
```

## VB .Net Signature:
```cs
Private Declare Function AccessibleObjectFromWindow Lib "oleacc" (ByVal Hwnd As Int32, _
    ByVal dwId As Int32, _
    ByRef riid As Guid, _
    <MarshalAs(UnmanagedType.IUnknown)> ByRef ppvObject As Object) As Int32
```

## Visual Basic
```cs
Private Declare Function AccessibleObjectFromWindow Lib "oleacc" (ByVal Hwnd As Int32, _
    ByVal dwId As Int32, _
    ByRef riid As Guid, _
    <MarshalAs(UnmanagedType.IUnknown)> ByRef ppvObject As Object) As Int32
    Declare Function GetForegroundWindow Lib "user32" () As Int32

    Private Sub Form2_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles MyBase.Load
    Dim varChild As Accessibility.IAccessible
    Dim hWnd As Int32 = GetForegroundWindow()
    Dim ID As Int32 = 0
    Dim IID_IAcce As Guid = New Guid("618736E0-3C3D-11CF-810C-00AA00389B71")
    Dim aaVal As Int32 = AccessibleObjectFromWindow(hWnd, ID, IID_IAcce, varChild)
    End Sub
```

## C#
```cs
internal enum OBJID : uint
    {
        WINDOW = 0x00000000,
        SYSMENU = 0xFFFFFFFF,
        TITLEBAR = 0xFFFFFFFE,
        MENU = 0xFFFFFFFD,
        CLIENT = 0xFFFFFFFC,
        VSCROLL = 0xFFFFFFFB,
        HSCROLL = 0xFFFFFFFA,
        SIZEGRIP = 0xFFFFFFF9,
        CARET = 0xFFFFFFF8,
        CURSOR = 0xFFFFFFF7,
        ALERT = 0xFFFFFFF6,
        SOUND = 0xFFFFFFF5,
    }

    Guid guid = new Guid("{618736E0-3C3D-11CF-810C-00AA00389B71}");
    object obj = null;
    int retVal = AccessibleObjectFromWindow(hwnd, (uint)OBJID.WINDOW, ref guid, ref obj);
    accessible = (IAccessible) obj;
```
