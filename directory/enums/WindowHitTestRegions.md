
## C# Definition:
```cs
/// <summary>
/// SOURCE: https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-nchittest#return-value
/// The return value of the DefWindowProc function, or the Message.Result value used in a WndProc(ref Message) method of a .NET WinForms Form object, is one of the following values, indicating the position of the cursor hot spot.
/// </summary>
enum  WindowHitTestRegions {
   /// <summary>In the border of a window that does not have a sizing border.</summary>
    HTBORDER = 18,
    /// <summary>In the lower-horizontal border of a resizable window (the user can click the mouse to resize the window vertically).</summary>
    HTBOTTOM = 15,
    /// <summary>In the lower-left corner of a border of a resizable window (the user can click the mouse to resize the window diagonally).</summary>
    HTBOTTOMLEFT = 16,
    /// <summary>In the lower-right corner of a border of a resizable window (the user can click the mouse to resize the window diagonally).</summary>
    HTBOTTOMRIGHT = 17,
    /// <summary>In a title bar.</summary>
    HTCAPTION = 2,
    /// <summary>In a client area.</summary>
    HTCLIENT = 1,
    /// <summary>In a Close button.</summary>
    HTCLOSE = 20,
    /// <summary>On the screen background or on a dividing line between windows (same as HTNOWHERE, except that the DefWindowProc function produces a system beep to indicate an error).</summary>
    HTERROR = -2,
    /// <summary>In a size box (same as HTSIZE).</summary>
    HTGROWBOX = 4,
    /// <summary>In a Help button.</summary>
    HTHELP = 21,
    /// <summary>In a horizontal scroll bar.</summary>
    HTHSCROLL = 6,
    /// <summary>In the left border of a resizable window (the user can click the mouse to resize the window horizontally).</summary>
    HTLEFT = 10,
    /// <summary>In a menu.</summary>
    HTMENU = 5,
    /// <summary>In a Maximize button.</summary>
    HTMAXBUTTON = 9,
    /// <summary>In a Minimize button.</summary>
    HTMINBUTTON = 8,
    /// <summary>On the screen background or on a dividing line between windows.</summary>
    HTNOWHERE = 0,
    /// <summary>In a Minimize button.</summary>
    HTREDUCE = 8,
    /// <summary>In the right border of a resizable window (the user can click the mouse to resize the window horizontally).</summary>
    HTRIGHT = 11,
    /// <summary>In a size box (same as HTGROWBOX).</summary>
    HTSIZE = 4,
    /// <summary>In a window menu or in a Close button in a child window.</summary>
    HTSYSMENU = 3,
    /// <summary>In the upper-horizontal border of a window.</summary>
    HTTOP = 12,
    /// <summary>In the upper-left corner of a window border.</summary>
    HTTOPLEFT = 13,
    /// <summary>In the upper-right corner of a window border.</summary>
    HTTOPRIGHT = 14,
    /// <summary>In a window currently covered by another window in the same thread (the message will be sent to underlying windows in the same thread until one of them returns a code that is not HTTRANSPARENT).</summary>
    HTTRANSPARENT = -1,
    /// <summary>In the vertical scroll bar.</summary>
    HTVSCROLL = 7,
    /// <summary>In a Maximize button.</summary>
    HTZOOM = 9,
}
```

## VB Definition:
```cs
Enum  WindowHitTestRegions
   TODO
End Enum
```
