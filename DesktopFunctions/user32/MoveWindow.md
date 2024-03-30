
## C# Signature:
```cs
/// <summary>
///     The MoveWindow function changes the position and dimensions of the specified window. For a top-level window, the
///     position and dimensions are relative to the upper-left corner of the screen. For a child window, they are relative
///     to the upper-left corner of the parent window's client area.
///     <para>
///     Go to https://msdn.microsoft.com/en-us/library/windows/desktop/ms633534%28v=vs.85%29.aspx for more
///     information
///     </para>
/// </summary>
/// <param name="hWnd">C++ ( hWnd [in]. Type: HWND )<br /> Handle to the window.</param>
/// <param name="X">C++ ( X [in]. Type: int )<br />Specifies the new position of the left side of the window.</param>
/// <param name="Y">C++ ( Y [in]. Type: int )<br /> Specifies the new position of the top of the window.</param>
/// <param name="nWidth">C++ ( nWidth [in]. Type: int )<br />Specifies the new width of the window.</param>
/// <param name="nHeight">C++ ( nHeight [in]. Type: int )<br />Specifies the new height of the window.</param>
/// <param name="bRepaint">
///     C++ ( bRepaint [in]. Type: bool )<br />Specifies whether the window is to be repainted. If this
///     parameter is TRUE, the window receives a message. If the parameter is FALSE, no repainting of any kind occurs. This
///     applies to the client area, the nonclient area (including the title bar and scroll bars), and any part of the
///     parent window uncovered as a result of moving a child window.
/// </param>
/// <returns>
///     If the function succeeds, the return value is nonzero.<br /> If the function fails, the return value is zero.
///     <br />To get extended error information, call GetLastError.
/// </returns>
[DllImport("user32.dll", SetLastError = true)]
internal static extern bool MoveWindow(IntPtr hWnd, int X, int Y, int nWidth, int nHeight, bool bRepaint);
```

## VB.Net Signature:
```cs
''' <summary>
    ''' The MoveWindow function changes the position and dimensions of the specified window. For a top-level window, the position and dimensions are relative to the upper-left corner of the screen. For a child window, they are relative to the upper-left corner of the parent window's client area.
    ''' </summary>
    ''' <param name="hWnd">Handle to the window.</param>
    ''' <param name="X">Specifies the new position of the left side of the window.</param>
    ''' <param name="Y">Specifies the new position of the top of the window.</param>
    ''' <param name="nWidth">Specifies the new width of the window.</param>
    ''' <param name="nHeight">Specifies the new height of the window.</param>
    ''' <param name="bRepaint">Specifies whether the window is to be repainted. If this parameter is TRUE, the window receives a message. If the parameter is FALSE, no repainting of any kind occurs. This applies to the client area, the nonclient area (including the title bar and scroll bars), and any part of the parent window uncovered as a result of moving a child window.</param>
    ''' <returns>If the function succeeds, the return value is nonzero.
    ''' <para>If the function fails, the return value is zero. To get extended error information, call GetLastError.</para></returns>
    <DllImport("user32.dll")> _
    Public Shared Function MoveWindow(ByVal hWnd As IntPtr, ByVal x As Integer, ByVal y As Integer, ByVal nWidth As Integer, ByVal nHeight As Integer, ByVal bRepaint As Boolean) As Boolean
    End Function
```

## C++ Signature:
```cs
[DllImport("User32.dll")]
extern bool MoveWindow(IntPtr handle, int x, int y, int width, int height, bool redraw);
```

## Sample Code:
```cs
class Program
    {
    internal struct RECT
    {
        public int left;
        public int top;
        public int right;
        public int bottom;
    }

    [DllImport("user32.dll", ExactSpelling = true, SetLastError = true)]
    internal static extern IntPtr GetForegroundWindow();

    [DllImport("user32.dll", CharSet = CharSet.Auto, CallingConvention = CallingConvention.StdCall, ExactSpelling = true, SetLastError = true)]
    internal static extern bool GetWindowRect(IntPtr hWnd, ref RECT rect);

    [DllImport("user32.dll", CharSet = CharSet.Auto, CallingConvention = CallingConvention.StdCall, ExactSpelling = true, SetLastError = true)]
    internal static extern void MoveWindow(IntPtr hwnd, int X, int Y, int nWidth, int nHeight, bool bRepaint);

    static void Main(string[] args)
    {
        IntPtr id;
        RECT Rect = new RECT();
        Thread.Sleep(2000);
        id = GetForegroundWindow();
        Random myRandom = new Random();
        GetWindowRect(id, ref Rect);
        MoveWindow(id, myRandom.Next(1024), myRandom.Next(768), Rect.right - Rect.left, Rect.bottom - Rect.top, true);

    }
    }
```

## Sample Code:
```cs
Public Declare Auto Function MoveWindow Lib "user32.dll" ( _
    ByVal hWnd As IntPtr, _
    ByVal X As Int32, _
    ByVal Y As Int32, _
    ByVal nWidth As Int32, _
    ByVal nHeight As Int32, _
    ByVal bRepaint As Boolean _
    ) As Boolean
```

## Sample Code:
```cs
Private Sub ResizeMe_MouseMove(ByVal sender As Object, ByVal e As System.Windows.Forms.MouseEventArgs) Handles ResizeMe.MouseMove

    If e.Button = MouseButtons.Left Then

    MoveWindow(Me.Handle, Me.Location.X, Me.Location.Y, (Control.MousePosition.X - (Me.Left)) + 10, (Control.MousePosition.Y - Me.Top) + 10, True)
    Me.Refresh()
    System.Windows.Forms.Application.DoEvents()

    End If
```

## Additional Uses (Contributed by Hayden B):
```cs
Public Declare Auto Function MoveWindow Lib "user32.dll" ( _
      ByVal hWnd As IntPtr, _
      ByVal X As Int32, _
      ByVal Y As Int32, _
      ByVal nWidth As Int32, _
      ByVal nHeight As Int32, _
      ByVal bRepaint As Boolean _
      ) As Boolean
    Private InitX As Integer
    Private LR As String = "L"
    Private C As Integer = 0
    Private X As Integer = 0

    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
    InitX = Me.Location.X
    X = InitX
    C = 0
    Timer1.Interval = 1
    Timer1.Start()
    End Sub

    Private Sub Timer1_Tick(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Timer1.Tick
    C += 1
    If X = InitX - 6 Then
        LR = "R"
    ElseIf X = InitX + 6 Then
        LR = "L"
    End If

    If LR = "L" Then
        X -= 2
    Else
        X += 2
    End If

    MoveWindow(Me.Handle, X, Me.Location.Y, Me.Width, Me.Height, True)
    Me.Refresh()
    System.Windows.Forms.Application.DoEvents()
    If C = 30 Then
        Timer1.Stop()
    End If
    End Sub
The MoveWindow API3/28/2016 1:39:06 PM - -67.166.68.151TODO - a short description of this collection of constants4/6/2012 12:59:20 AM - anonymousTODO - a short description of this collection of constants4/6/2012 12:59:20 AM - anonymous
```
