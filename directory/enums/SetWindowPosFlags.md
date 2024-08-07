
## C# Definition:
```cs
[Flags()]
private enum SetWindowPosFlags : uint
{
    /// <summary>If the calling thread and the thread that owns the window are attached to different input queues, 
    /// the system posts the request to the thread that owns the window. This prevents the calling thread from 
    /// blocking its execution while other threads process the request.</summary>
    /// <remarks>SWP_ASYNCWINDOWPOS</remarks>
    AsynchronousWindowPosition = 0x4000,
    /// <summary>Prevents generation of the WM_SYNCPAINT message.</summary>
    /// <remarks>SWP_DEFERERASE</remarks>
    DeferErase = 0x2000,
    /// <summary>Draws a frame (defined in the window's class description) around the window.</summary>
    /// <remarks>SWP_DRAWFRAME</remarks>
    DrawFrame = 0x0020,
    /// <summary>Applies new frame styles set using the SetWindowLong function. Sends a WM_NCCALCSIZE message to 
    /// the window, even if the window's size is not being changed. If this flag is not specified, WM_NCCALCSIZE 
    /// is sent only when the window's size is being changed.</summary>
    /// <remarks>SWP_FRAMECHANGED</remarks>
    FrameChanged = 0x0020,
    /// <summary>Hides the window.</summary>
    /// <remarks>SWP_HIDEWINDOW</remarks>
    HideWindow = 0x0080,
    /// <summary>Does not activate the window. If this flag is not set, the window is activated and moved to the 
    /// top of either the topmost or non-topmost group (depending on the setting of the hWndInsertAfter 
    /// parameter).</summary>
    /// <remarks>SWP_NOACTIVATE</remarks>
    DoNotActivate = 0x0010,
    /// <summary>Discards the entire contents of the client area. If this flag is not specified, the valid 
    /// contents of the client area are saved and copied back into the client area after the window is sized or 
    /// repositioned.</summary>
    /// <remarks>SWP_NOCOPYBITS</remarks>
    DoNotCopyBits = 0x0100,
    /// <summary>Retains the current position (ignores X and Y parameters).</summary>
    /// <remarks>SWP_NOMOVE</remarks>
    IgnoreMove = 0x0002,
    /// <summary>Does not change the owner window's position in the Z order.</summary>
    /// <remarks>SWP_NOOWNERZORDER</remarks>
    DoNotChangeOwnerZOrder = 0x0200,
    /// <summary>Does not redraw changes. If this flag is set, no repainting of any kind occurs. This applies to 
    /// the client area, the nonclient area (including the title bar and scroll bars), and any part of the parent 
    /// window uncovered as a result of the window being moved. When this flag is set, the application must 
    /// explicitly invalidate or redraw any parts of the window and parent window that need redrawing.</summary>
    /// <remarks>SWP_NOREDRAW</remarks>
    DoNotRedraw = 0x0008,
    /// <summary>Same as the SWP_NOOWNERZORDER flag.</summary>
    /// <remarks>SWP_NOREPOSITION</remarks>
    DoNotReposition = 0x0200,
    /// <summary>Prevents the window from receiving the WM_WINDOWPOSCHANGING message.</summary>
    /// <remarks>SWP_NOSENDCHANGING</remarks>
    DoNotSendChangingEvent = 0x0400,
    /// <summary>Retains the current size (ignores the cx and cy parameters).</summary>
    /// <remarks>SWP_NOSIZE</remarks>
    IgnoreResize = 0x0001,
    /// <summary>Retains the current Z order (ignores the hWndInsertAfter parameter).</summary>
    /// <remarks>SWP_NOZORDER</remarks>
    IgnoreZOrder = 0x0004,
    /// <summary>Displays the window.</summary>
    /// <remarks>SWP_SHOWWINDOW</remarks>
    ShowWindow = 0x0040,
}
```

## VB.NET Definition:
```cs
<Flags> _
Private Enum SetWindowPosFlags As UInteger
    ''' <summary>If the calling thread and the thread that owns the window are attached to different input queues, 
    ''' the system posts the request to the thread that owns the window. This prevents the calling thread from 
    ''' blocking its execution while other threads process the request.</summary>
    ''' <remarks>SWP_ASYNCWINDOWPOS</remarks>
    SynchronousWindowPosition = &H4000
    ''' <summary>Prevents generation of the WM_SYNCPAINT message.</summary>
    ''' <remarks>SWP_DEFERERASE</remarks>
    DeferErase = &H2000
    ''' <summary>Draws a frame (defined in the window's class description) around the window.</summary>
    ''' <remarks>SWP_DRAWFRAME</remarks>
    DrawFrame = &H20
    ''' <summary>Applies new frame styles set using the SetWindowLong function. Sends a WM_NCCALCSIZE message to 
    ''' the window, even if the window's size is not being changed. If this flag is not specified, WM_NCCALCSIZE 
    ''' is sent only when the window's size is being changed.</summary>
    ''' <remarks>SWP_FRAMECHANGED</remarks>
    FrameChanged = &H20
    ''' <summary>Hides the window.</summary>
    ''' <remarks>SWP_HIDEWINDOW</remarks>
    HideWindow = &H80
    ''' <summary>Does not activate the window. If this flag is not set, the window is activated and moved to the 
    ''' top of either the topmost or non-topmost group (depending on the setting of the hWndInsertAfter 
    ''' parameter).</summary>
    ''' <remarks>SWP_NOACTIVATE</remarks>
    DoNotActivate = &H10
    ''' <summary>Discards the entire contents of the client area. If this flag is not specified, the valid 
    ''' contents of the client area are saved and copied back into the client area after the window is sized or 
    ''' repositioned.</summary>
    ''' <remarks>SWP_NOCOPYBITS</remarks>
    DoNotCopyBits = &H100
    ''' <summary>Retains the current position (ignores X and Y parameters).</summary>
    ''' <remarks>SWP_NOMOVE</remarks>
    IgnoreMove = &H2
    ''' <summary>Does not change the owner window's position in the Z order.</summary>
    ''' <remarks>SWP_NOOWNERZORDER</remarks>
    DoNotChangeOwnerZOrder = &H200
    ''' <summary>Does not redraw changes. If this flag is set, no repainting of any kind occurs. This applies to 
    ''' the client area, the nonclient area (including the title bar and scroll bars), and any part of the parent 
    ''' window uncovered as a result of the window being moved. When this flag is set, the application must 
    ''' explicitly invalidate or redraw any parts of the window and parent window that need redrawing.</summary>
    ''' <remarks>SWP_NOREDRAW</remarks>
    DoNotRedraw = &H8
    ''' <summary>Same as the SWP_NOOWNERZORDER flag.</summary>
    ''' <remarks>SWP_NOREPOSITION</remarks>
    DoNotReposition = &H200
    ''' <summary>Prevents the window from receiving the WM_WINDOWPOSCHANGING message.</summary>
    ''' <remarks>SWP_NOSENDCHANGING</remarks>
    DoNotSendChangingEvent = &H400
    ''' <summary>Retains the current size (ignores the cx and cy parameters).</summary>
    ''' <remarks>SWP_NOSIZE</remarks>
    IgnoreResize = &H1
    ''' <summary>Retains the current Z order (ignores the hWndInsertAfter parameter).</summary>
    ''' <remarks>SWP_NOZORDER</remarks>
    IgnoreZOrder = &H4
    ''' <summary>Displays the window.</summary>
    ''' <remarks>SWP_SHOWWINDOW</remarks>
    ShowWindow = &H40
End Enum
```
