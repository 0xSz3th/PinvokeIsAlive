
## C# Signature:
```cs
/// <summary>
    ///     Changes the size, position, and Z order of a child, pop-up, or top-level window. These windows are ordered
    ///     according to their appearance on the screen. The topmost window receives the highest rank and is the first window
    ///     in the Z order.
    ///     <para>See https://msdn.microsoft.com/en-us/library/windows/desktop/ms633545%28v=vs.85%29.aspx for more information.</para>
    /// </summary>
    /// <param name="hWnd">C++ ( hWnd [in]. Type: HWND )<br />A handle to the window.</param>
    /// <param name="hWndInsertAfter">
    ///     C++ ( hWndInsertAfter [in, optional]. Type: HWND )<br />A handle to the window to precede the positioned window in
    ///     the Z order. This parameter must be a window handle or one of the following values.
    ///     <list type="table">
    ///     <itemheader>
    ///         <term>HWND placement</term><description>Window to precede placement</description>
    ///     </itemheader>
    ///     <item>
    ///         <term>HWND_BOTTOM ((HWND)1)</term>
    ///         <description>
    ///         Places the window at the bottom of the Z order. If the hWnd parameter identifies a topmost
    ///         window, the window loses its topmost status and is placed at the bottom of all other windows.
    ///         </description>
    ///     </item>
    ///     <item>
    ///         <term>HWND_NOTOPMOST ((HWND)-2)</term>
    ///         <description>
    ///         Places the window above all non-topmost windows (that is, behind all topmost windows). This
    ///         flag has no effect if the window is already a non-topmost window.
    ///         </description>
    ///     </item>
    ///     <item>
    ///         <term>HWND_TOP ((HWND)0)</term><description>Places the window at the top of the Z order.</description>
    ///     </item>
    ///     <item>
    ///         <term>HWND_TOPMOST ((HWND)-1)</term>
    ///         <description>
    ///         Places the window above all non-topmost windows. The window maintains its topmost position
    ///         even when it is deactivated.
    ///         </description>
    ///     </item>
    ///     </list>
    ///     <para>For more information about how this parameter is used, see the following Remarks section.</para>
    /// </param>
    /// <param name="X">C++ ( X [in]. Type: int )<br />The new position of the left side of the window, in client coordinates.</param>
    /// <param name="Y">C++ ( Y [in]. Type: int )<br />The new position of the top of the window, in client coordinates.</param>
    /// <param name="cx">C++ ( cx [in]. Type: int )<br />The new width of the window, in pixels.</param>
    /// <param name="cy">C++ ( cy [in]. Type: int )<br />The new height of the window, in pixels.</param>
    /// <param name="uFlags">
    ///     C++ ( uFlags [in]. Type: UINT )<br />The window sizing and positioning flags. This parameter can be a combination
    ///     of the following values.
    ///     <list type="table">
    ///     <itemheader>
    ///         <term>HWND sizing and positioning flags</term>
    ///         <description>Where to place and size window. Can be a combination of any</description>
    ///     </itemheader>
    ///     <item>
    ///         <term>SWP_ASYNCWINDOWPOS (0x4000)</term>
    ///         <description>
    ///         If the calling thread and the thread that owns the window are attached to different input
    ///         queues, the system posts the request to the thread that owns the window. This prevents the calling
    ///         thread from blocking its execution while other threads process the request.
    ///         </description>
    ///     </item>
    ///     <item>
    ///         <term>SWP_DEFERERASE (0x2000)</term>
    ///         <description>Prevents generation of the WM_SYNCPAINT message. </description>
    ///     </item>
    ///     <item>
    ///         <term>SWP_DRAWFRAME (0x0020)</term>
    ///         <description>Draws a frame (defined in the window's class description) around the window.</description>
    ///     </item>
    ///     <item>
    ///         <term>SWP_FRAMECHANGED (0x0020)</term>
    ///         <description>
    ///         Applies new frame styles set using the SetWindowLong function. Sends a WM_NCCALCSIZE message
    ///         to the window, even if the window's size is not being changed. If this flag is not specified,
    ///         WM_NCCALCSIZE is sent only when the window's size is being changed
    ///         </description>
    ///     </item>
    ///     <item>
    ///         <term>SWP_HIDEWINDOW (0x0080)</term><description>Hides the window.</description>
    ///     </item>
    ///     <item>
    ///         <term>SWP_NOACTIVATE (0x0010)</term>
    ///         <description>
    ///         Does not activate the window. If this flag is not set, the window is activated and moved to
    ///         the top of either the topmost or non-topmost group (depending on the setting of the hWndInsertAfter
    ///         parameter).
    ///         </description>
    ///     </item>
    ///     <item>
    ///         <term>SWP_NOCOPYBITS (0x0100)</term>
    ///         <description>
    ///         Discards the entire contents of the client area. If this flag is not specified, the valid
    ///         contents of the client area are saved and copied back into the client area after the window is sized or
    ///         repositioned.
    ///         </description>
    ///     </item>
    ///     <item>
    ///         <term>SWP_NOMOVE (0x0002)</term>
    ///         <description>Retains the current position (ignores X and Y parameters).</description>
    ///     </item>
    ///     <item>
    ///         <term>SWP_NOOWNERZORDER (0x0200)</term>
    ///         <description>Does not change the owner window's position in the Z order.</description>
    ///     </item>
    ///     <item>
    ///         <term>SWP_NOREDRAW (0x0008)</term>
    ///         <description>
    ///         Does not redraw changes. If this flag is set, no repainting of any kind occurs. This applies
    ///         to the client area, the nonclient area (including the title bar and scroll bars), and any part of the
    ///         parent window uncovered as a result of the window being moved. When this flag is set, the application
    ///         must explicitly invalidate or redraw any parts of the window and parent window that need redrawing.
    ///         </description>
    ///     </item>
    ///     <item>
    ///         <term>SWP_NOREPOSITION (0x0200)</term><description>Same as the SWP_NOOWNERZORDER flag.</description>
    ///     </item>
    ///     <item>
    ///         <term>SWP_NOSENDCHANGING (0x0400)</term>
    ///         <description>Prevents the window from receiving the WM_WINDOWPOSCHANGING message.</description>
    ///     </item>
    ///     <item>
    ///         <term>SWP_NOSIZE (0x0001)</term>
    ///         <description>Retains the current size (ignores the cx and cy parameters).</description>
    ///     </item>
    ///     <item>
    ///         <term>SWP_NOZORDER (0x0004)</term>
    ///         <description>Retains the current Z order (ignores the hWndInsertAfter parameter).</description>
    ///     </item>
    ///     <item>
    ///         <term>SWP_SHOWWINDOW (0x0040)</term><description>Displays the window.</description>
    ///     </item>
    ///     </list>
    /// </param>
    /// <returns><c>true</c> or nonzero if the function succeeds, <c>false</c> or zero otherwise or if function fails.</returns>
    /// <remarks>
    ///     <para>
    ///     As part of the Vista re-architecture, all services were moved off the interactive desktop into Session 0.
    ///     hwnd and window manager operations are only effective inside a session and cross-session attempts to manipulate
    ///     the hwnd will fail. For more information, see The Windows Vista Developer Story: Application Compatibility
    ///     Cookbook.
    ///     </para>
    ///     <para>
    ///     If you have changed certain window data using SetWindowLong, you must call SetWindowPos for the changes to
    ///     take effect. Use the following combination for uFlags: SWP_NOMOVE | SWP_NOSIZE | SWP_NOZORDER |
    ///     SWP_FRAMECHANGED.
    ///     </para>
    ///     <para>
    ///     A window can be made a topmost window either by setting the hWndInsertAfter parameter to HWND_TOPMOST and
    ///     ensuring that the SWP_NOZORDER flag is not set, or by setting a window's position in the Z order so that it is
    ///     above any existing topmost windows. When a non-topmost window is made topmost, its owned windows are also made
    ///     topmost. Its owners, however, are not changed.
    ///     </para>
    ///     <para>
    ///     If neither the SWP_NOACTIVATE nor SWP_NOZORDER flag is specified (that is, when the application requests that
    ///     a window be simultaneously activated and its position in the Z order changed), the value specified in
    ///     hWndInsertAfter is used only in the following circumstances.
    ///     </para>
    ///     <list type="bullet">
    ///     <item>Neither the HWND_TOPMOST nor HWND_NOTOPMOST flag is specified in hWndInsertAfter. </item>
    ///     <item>The window identified by hWnd is not the active window. </item>
    ///     </list>
    ///     <para>
    ///     An application cannot activate an inactive window without also bringing it to the top of the Z order.
    ///     Applications can change an activated window's position in the Z order without restrictions, or it can activate
    ///     a window and then move it to the top of the topmost or non-topmost windows.
    ///     </para>
    ///     <para>
    ///     If a topmost window is repositioned to the bottom (HWND_BOTTOM) of the Z order or after any non-topmost
    ///     window, it is no longer topmost. When a topmost window is made non-topmost, its owners and its owned windows
    ///     are also made non-topmost windows.
    ///     </para>
    ///     <para>
    ///     A non-topmost window can own a topmost window, but the reverse cannot occur. Any window (for example, a
    ///     dialog box) owned by a topmost window is itself made a topmost window, to ensure that all owned windows stay
    ///     above their owner.
    ///     </para>
    ///     <para>
    ///     If an application is not in the foreground, and should be in the foreground, it must call the
    ///     SetForegroundWindow function.
    ///     </para>
    ///     <para>
    ///     To use SetWindowPos to bring a window to the top, the process that owns the window must have
    ///     SetForegroundWindow permission.
    ///     </para>
    /// </remarks>

[DllImport("user32.dll", SetLastError=true)]
static extern bool SetWindowPos(IntPtr hWnd, IntPtr hWndInsertAfter, int X, int Y, int cx, int cy, UInt32 uFlags);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", SetLastError:=True)> _
Private Shared Function SetWindowPos(ByVal hWnd As IntPtr, ByVal hWndInsertAfter As IntPtr, ByVal X As Integer, ByVal Y As Integer, ByVal cx As Integer, ByVal cy As Integer, ByVal uFlags As UInt32) As Boolean
End Function
```

## VB Signature
```cs
Public Declare Function SetWindowPos Lib "user32.dll" _
         (ByVal hWnd As Long, _
          ByVal hWndInsertAfter As Long, _
          ByVal X As Long, _
          ByVal Y As Long, _
          ByVal cx As Long, _
          ByVal cy As Long, _
          ByVal wFlags As Long) As Long
```

## C# Constants:
```cs
static readonly IntPtr HWND_TOPMOST = new IntPtr(-1);
static readonly IntPtr HWND_NOTOPMOST = new IntPtr(-2);
static readonly IntPtr HWND_TOP = new IntPtr(0);
static readonly IntPtr HWND_BOTTOM = new IntPtr(1);

/// <summary>
/// Window handles (HWND) used for hWndInsertAfter
/// </summary>
public static class HWND
{
   public static IntPtr
   NoTopMost = new IntPtr(-2),
   TopMost = new IntPtr(-1),
   Top = new IntPtr(0),
   Bottom = new IntPtr(1);
}

/// <summary>
/// SetWindowPos Flags
/// </summary>
public static class SWP
{
   public static readonly int
   NOSIZE = 0x0001,
   NOMOVE = 0x0002,
   NOZORDER = 0x0004,
   NOREDRAW = 0x0008,
   NOACTIVATE = 0x0010,
   DRAWFRAME = 0x0020,
   FRAMECHANGED = 0x0020,
   SHOWWINDOW = 0x0040,
   HIDEWINDOW = 0x0080,
   NOCOPYBITS = 0x0100,
   NOOWNERZORDER = 0x0200,
   NOREPOSITION = 0x0200,
   NOSENDCHANGING = 0x0400,
   DEFERERASE = 0x2000,
   ASYNCWINDOWPOS = 0x4000;
}
```

## VB.NET Constants:
```cs
Private ReadOnly HWND_BOTTOM As New IntPtr(1)
Private ReadOnly HWND_NOTOPMOST As New IntPtr(-2)
Private ReadOnly HWND_TOP As New IntPtr(0)
Private ReadOnly HWND_TOPMOST As New IntPtr(-1)
```

## Alternative Managed API:
```cs
/// <summary>
    ///     Special window handles
    /// </summary>
    public enum SpecialWindowHandles
    {
        // ReSharper disable InconsistentNaming
        /// <summary>
        ///     Places the window at the top of the Z order.
        /// </summary>
        HWND_TOP = 0,
        /// <summary>
        ///     Places the window at the bottom of the Z order. If the hWnd parameter identifies a topmost window, the window loses its topmost status and is placed at the bottom of all other windows.
        /// </summary>
        HWND_BOTTOM = 1,
        /// <summary>
        ///     Places the window above all non-topmost windows. The window maintains its topmost position even when it is deactivated.
        /// </summary>
        HWND_TOPMOST = -1,
        /// <summary>
        ///     Places the window above all non-topmost windows (that is, behind all topmost windows). This flag has no effect if the window is already a non-topmost window.
        /// </summary>
        HWND_NOTOPMOST = -2
        // ReSharper restore InconsistentNaming
    }

    [Flags]
    public enum SetWindowPosFlags : uint
    {
        // ReSharper disable InconsistentNaming

        /// <summary>
        ///     If the calling thread and the thread that owns the window are attached to different input queues, the system posts the request to the thread that owns the window. This prevents the calling thread from blocking its execution while other threads process the request.
        /// </summary>
        SWP_ASYNCWINDOWPOS = 0x4000,

        /// <summary>
        ///     Prevents generation of the WM_SYNCPAINT message.
        /// </summary>
        SWP_DEFERERASE = 0x2000,

        /// <summary>
        ///     Draws a frame (defined in the window's class description) around the window.
        /// </summary>
        SWP_DRAWFRAME = 0x0020,

        /// <summary>
        ///     Applies new frame styles set using the SetWindowLong function. Sends a WM_NCCALCSIZE message to the window, even if the window's size is not being changed. If this flag is not specified, WM_NCCALCSIZE is sent only when the window's size is being changed.
        /// </summary>
        SWP_FRAMECHANGED = 0x0020,

        /// <summary>
        ///     Hides the window.
        /// </summary>
        SWP_HIDEWINDOW = 0x0080,

        /// <summary>
        ///     Does not activate the window. If this flag is not set, the window is activated and moved to the top of either the topmost or non-topmost group (depending on the setting of the hWndInsertAfter parameter).
        /// </summary>
        SWP_NOACTIVATE = 0x0010,

        /// <summary>
        ///     Discards the entire contents of the client area. If this flag is not specified, the valid contents of the client area are saved and copied back into the client area after the window is sized or repositioned.
        /// </summary>
        SWP_NOCOPYBITS = 0x0100,

        /// <summary>
        ///     Retains the current position (ignores X and Y parameters).
        /// </summary>
        SWP_NOMOVE = 0x0002,

        /// <summary>
        ///     Does not change the owner window's position in the Z order.
        /// </summary>
        SWP_NOOWNERZORDER = 0x0200,

        /// <summary>
        ///     Does not redraw changes. If this flag is set, no repainting of any kind occurs. This applies to the client area, the nonclient area (including the title bar and scroll bars), and any part of the parent window uncovered as a result of the window being moved. When this flag is set, the application must explicitly invalidate or redraw any parts of the window and parent window that need redrawing.
        /// </summary>
        SWP_NOREDRAW = 0x0008,

        /// <summary>
        ///     Same as the SWP_NOOWNERZORDER flag.
        /// </summary>
        SWP_NOREPOSITION = 0x0200,

        /// <summary>
        ///     Prevents the window from receiving the WM_WINDOWPOSCHANGING message.
        /// </summary>
        SWP_NOSENDCHANGING = 0x0400,

        /// <summary>
        ///     Retains the current size (ignores the cx and cy parameters).
        /// </summary>
        SWP_NOSIZE = 0x0001,

        /// <summary>
        ///     Retains the current Z order (ignores the hWndInsertAfter parameter).
        /// </summary>
        SWP_NOZORDER = 0x0004,

        /// <summary>
        ///     Displays the window.
        /// </summary>
        SWP_SHOWWINDOW = 0x0040,

        // ReSharper restore InconsistentNaming
    }
```

## C# Code Sample
```cs
public static void MoveWindowToMonitor(int monitor)
    {
        var windowHandler = GetActiveWindowHandle();

        var windowRec = GetWindowRect(windowHandler);
        // When I move a window to a different monitor it subtracts 16 from the Width and 38 from the Height, Not sure if this is on my system or others.
        SetWindowPos(windowHandler, (IntPtr)SpecialWindowHandles.HWND_TOP, Screen.AllScreens[monitor].WorkingArea.Left,
             Screen.AllScreens[monitor].WorkingArea.Top, windowRec.Size.Width + 16, windowRec.Size.Height + 38,
             SetWindowPosFlags.SWP_SHOWWINDOW);
    }
```

## VB.Net Sample
```cs
Const HWND_TOP = 0          'Places the window at the top of the Z order
    Const HWND_BOTTOM = 1       'Places the window at the bottom of the Z order. If the hWnd parameter identifies a topmost window, the window loses its topmost status and is placed at the bottom of all other windows.
    Const HWND_TOPMOST = -1     'Places the window above all non-topmost windows. The window maintains its topmost position even when it is deactivated.
    Const HWND_NOTOPMOST = -2       'Places the window above all non-topmost windows (that is, behind all topmost windows). This flag has no effect if the window is already a non-topmost window.
```

## VB.Net Sample
```cs
Const SWP_NOSIZE = &H1      'Retains the current size (ignores the cx and cy parameters).
    Const SWP_NOMOVE = &H2      'Retains the current position (ignores X and Y parameters).
    Const SWP_NOZORDER = &H4    'Retains the current Z order (ignores the hWndInsertAfter parameter).
    Const SWP_NOACTIVATE = &H10     'Does not activate the window. If this flag is not set, the window is activated and moved to the top of either the topmost or non-topmost group (depending on the setting of the hWndInsertAfter parameter).
    Const SWP_SHOWWINDOW = &H40     'Displays the window.
    Const SWP_HIDEWINDOW = &H80     'Hides the window.
    Const SWP_NOOWNERZORDER = &H200 'Does not change the owner window's position in the Z order.

    'see if the notepad window is there
    Dim hWnd As IntPtr = 0
    hWnd = FindWindowExW(IntPtr.Zero, IntPtr.Zero, Nothing, "Untitled - Notepad")

    If hWnd = 0 Then
        MessageBox.Show("Notepad window not found")
    Else
        SetWindowPos(hWnd, HWND_NOTOPMOST, 10, 10, 0, 0, SWP_NOSIZE Or SWP_NOACTIVATE)
    End If
```

## C# WPF Remarks
```cs
using System.Windows.Interop;
```

## C# WPF Remarks
```cs
WindowInteropHelper winHelp = new WindowInteropHelper(target);
```
