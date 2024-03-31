
## C# Definition:
```cs
/// <summary>
  /// Windows Messages
  /// Defined in winuser.h from Windows SDK v6.1
  /// Documentation pulled from MSDN.
  /// </summary>
  public enum WM : uint
  {
    /// <summary>
    /// The WM_NULL message performs no operation. An application sends the WM_NULL message if it wants to post a message that the recipient window will ignore.
    /// </summary>
    NULL = 0x0000,
    /// <summary>
    /// The WM_CREATE message is sent when an application requests that a window be created by calling the CreateWindowEx or CreateWindow function. (The message is sent before the function returns.) The window procedure of the new window receives this message after the window is created, but before the window becomes visible.
    /// </summary>
    CREATE = 0x0001,
    /// <summary>
    /// The WM_DESTROY message is sent when a window is being destroyed. It is sent to the window procedure of the window being destroyed after the window is removed from the screen. 
    /// This message is sent first to the window being destroyed and then to the child windows (if any) as they are destroyed. During the processing of the message, it can be assumed that all child windows still exist.
    /// /// </summary>
    DESTROY = 0x0002,
    /// <summary>
    /// The WM_MOVE message is sent after a window has been moved. 
    /// </summary>
    MOVE = 0x0003,
    /// <summary>
    /// The WM_SIZE message is sent to a window after its size has changed.
    /// </summary>
    SIZE = 0x0005,
    /// <summary>
    /// The WM_ACTIVATE message is sent to both the window being activated and the window being deactivated. If the windows use the same input queue, the message is sent synchronously, first to the window procedure of the top-level window being deactivated, then to the window procedure of the top-level window being activated. If the windows use different input queues, the message is sent asynchronously, so the window is activated immediately. 
    /// </summary>
    ACTIVATE = 0x0006,
    /// <summary>
    /// The WM_SETFOCUS message is sent to a window after it has gained the keyboard focus. 
    /// </summary>
    SETFOCUS = 0x0007,
    /// <summary>
    /// The WM_KILLFOCUS message is sent to a window immediately before it loses the keyboard focus. 
    /// </summary>
    KILLFOCUS = 0x0008,
    /// <summary>
    /// The WM_ENABLE message is sent when an application changes the enabled state of a window. It is sent to the window whose enabled state is changing. This message is sent before the EnableWindow function returns, but after the enabled state (WS_DISABLED style bit) of the window has changed. 
    /// </summary>
    ENABLE = 0x000A,
    /// <summary>
    /// An application sends the WM_SETREDRAW message to a window to allow changes in that window to be redrawn or to prevent changes in that window from being redrawn. 
    /// </summary>
    SETREDRAW = 0x000B,
    /// <summary>
    /// An application sends a WM_SETTEXT message to set the text of a window. 
    /// </summary>
    SETTEXT = 0x000C,
    /// <summary>
    /// An application sends a WM_GETTEXT message to copy the text that corresponds to a window into a buffer provided by the caller. 
    /// </summary>
    GETTEXT = 0x000D,
    /// <summary>
    /// An application sends a WM_GETTEXTLENGTH message to determine the length, in characters, of the text associated with a window. 
    /// </summary>
    GETTEXTLENGTH = 0x000E,
    /// <summary>
    /// The WM_PAINT message is sent when the system or another application makes a request to paint a portion of an application's window. The message is sent when the UpdateWindow or RedrawWindow function is called, or by the DispatchMessage function when the application obtains a WM_PAINT message by using the GetMessage or PeekMessage function. 
    /// </summary>
    PAINT = 0x000F,
    /// <summary>
    /// The WM_CLOSE message is sent as a signal that a window or an application should terminate.
    /// </summary>
    CLOSE = 0x0010,
    /// <summary>
    /// The WM_QUERYENDSESSION message is sent when the user chooses to end the session or when an application calls one of the system shutdown functions. If any application returns zero, the session is not ended. The system stops sending WM_QUERYENDSESSION messages as soon as one application returns zero.
    /// After processing this message, the system sends the WM_ENDSESSION message with the wParam parameter set to the results of the WM_QUERYENDSESSION message.
    /// </summary>
    QUERYENDSESSION = 0x0011,
    /// <summary>
    /// The WM_QUERYOPEN message is sent to an icon when the user requests that the window be restored to its previous size and position.
    /// </summary>
    QUERYOPEN = 0x0013,
    /// <summary>
    /// The WM_ENDSESSION message is sent to an application after the system processes the results of the WM_QUERYENDSESSION message. The WM_ENDSESSION message informs the application whether the session is ending.
    /// </summary>
    ENDSESSION = 0x0016,
    /// <summary>
    /// The WM_QUIT message indicates a request to terminate an application and is generated when the application calls the PostQuitMessage function. It causes the GetMessage function to return zero.
    /// </summary>
    QUIT = 0x0012,
    /// <summary>
    /// The WM_ERASEBKGND message is sent when the window background must be erased (for example, when a window is resized). The message is sent to prepare an invalidated portion of a window for painting. 
    /// </summary>
    ERASEBKGND = 0x0014,
    /// <summary>
    /// This message is sent to all top-level windows when a change is made to a system color setting. 
    /// </summary>
    SYSCOLORCHANGE = 0x0015,
    /// <summary>
    /// The WM_SHOWWINDOW message is sent to a window when the window is about to be hidden or shown.
    /// </summary>
    SHOWWINDOW = 0x0018,
    /// <summary>
    /// An application sends the WM_WININICHANGE message to all top-level windows after making a change to the WIN.INI file. The SystemParametersInfo function sends this message after an application uses the function to change a setting in WIN.INI.
    /// Note  The WM_WININICHANGE message is provided only for compatibility with earlier versions of the system. Applications should use the WM_SETTINGCHANGE message.
    /// </summary>
    WININICHANGE = 0x001A,
    /// <summary>
    /// An application sends the WM_WININICHANGE message to all top-level windows after making a change to the WIN.INI file. The SystemParametersInfo function sends this message after an application uses the function to change a setting in WIN.INI.
    /// Note  The WM_WININICHANGE message is provided only for compatibility with earlier versions of the system. Applications should use the WM_SETTINGCHANGE message.
    /// </summary>
    SETTINGCHANGE = WININICHANGE,
    /// <summary>
    /// The WM_DEVMODECHANGE message is sent to all top-level windows whenever the user changes device-mode settings. 
    /// </summary>
    DEVMODECHANGE = 0x001B,
    /// <summary>
    /// The WM_ACTIVATEAPP message is sent when a window belonging to a different application than the active window is about to be activated. The message is sent to the application whose window is being activated and to the application whose window is being deactivated.
    /// </summary>
    ACTIVATEAPP = 0x001C,
    /// <summary>
    /// An application sends the WM_FONTCHANGE message to all top-level windows in the system after changing the pool of font resources. 
    /// </summary>
    FONTCHANGE = 0x001D,
    /// <summary>
    /// A message that is sent whenever there is a change in the system time.
    /// </summary>
    TIMECHANGE = 0x001E,
    /// <summary>
    /// The WM_CANCELMODE message is sent to cancel certain modes, such as mouse capture. For example, the system sends this message to the active window when a dialog box or message box is displayed. Certain functions also send this message explicitly to the specified window regardless of whether it is the active window. For example, the EnableWindow function sends this message when disabling the specified window.
    /// </summary>
    CANCELMODE = 0x001F,
    /// <summary>
    /// The WM_SETCURSOR message is sent to a window if the mouse causes the cursor to move within a window and mouse input is not captured. 
    /// </summary>
    SETCURSOR = 0x0020,
    /// <summary>
    /// The WM_MOUSEACTIVATE message is sent when the cursor is in an inactive window and the user presses a mouse button. The parent window receives this message only if the child window passes it to the DefWindowProc function.
    /// </summary>
    MOUSEACTIVATE = 0x0021,
    /// <summary>
    /// The WM_CHILDACTIVATE message is sent to a child window when the user clicks the window's title bar or when the window is activated, moved, or sized.
    /// </summary>
    CHILDACTIVATE = 0x0022,
    /// <summary>
    /// The WM_QUEUESYNC message is sent by a computer-based training (CBT) application to separate user-input messages from other messages sent through the WH_JOURNALPLAYBACK Hook procedure. 
    /// </summary>
    QUEUESYNC = 0x0023,
    /// <summary>
    /// The WM_GETMINMAXINFO message is sent to a window when the size or position of the window is about to change. An application can use this message to override the window's default maximized size and position, or its default minimum or maximum tracking size. 
    /// </summary>
    GETMINMAXINFO = 0x0024,
    /// <summary>
    /// Windows NT 3.51 and earlier: The WM_PAINTICON message is sent to a minimized window when the icon is to be painted. This message is not sent by newer versions of Microsoft Windows, except in unusual circumstances explained in the Remarks.
    /// </summary>
    PAINTICON = 0x0026,
    /// <summary>
    /// Windows NT 3.51 and earlier: The WM_ICONERASEBKGND message is sent to a minimized window when the background of the icon must be filled before painting the icon. A window receives this message only if a class icon is defined for the window; otherwise, WM_ERASEBKGND is sent. This message is not sent by newer versions of Windows.
    /// </summary>
    ICONERASEBKGND = 0x0027,
    /// <summary>
    /// The WM_NEXTDLGCTL message is sent to a dialog box procedure to set the keyboard focus to a different control in the dialog box. 
    /// </summary>
    NEXTDLGCTL = 0x0028,
    /// <summary>
    /// The WM_SPOOLERSTATUS message is sent from Print Manager whenever a job is added to or removed from the Print Manager queue. 
    /// </summary>
    SPOOLERSTATUS = 0x002A,
    /// <summary>
    /// The WM_DRAWITEM message is sent to the parent window of an owner-drawn button, combo box, list box, or menu when a visual aspect of the button, combo box, list box, or menu has changed.
    /// </summary>
    DRAWITEM = 0x002B,
    /// <summary>
    /// The WM_MEASUREITEM message is sent to the owner window of a combo box, list box, list view control, or menu item when the control or menu is created.
    /// </summary>
    MEASUREITEM = 0x002C,
    /// <summary>
    /// Sent to the owner of a list box or combo box when the list box or combo box is destroyed or when items are removed by the LB_DELETESTRING, LB_RESETCONTENT, CB_DELETESTRING, or CB_RESETCONTENT message. The system sends a WM_DELETEITEM message for each deleted item. The system sends the WM_DELETEITEM message for any deleted list box or combo box item with nonzero item data.
    /// </summary>
    DELETEITEM = 0x002D,
    /// <summary>
    /// Sent by a list box with the LBS_WANTKEYBOARDINPUT style to its owner in response to a WM_KEYDOWN message. 
    /// </summary>
    VKEYTOITEM = 0x002E,
    /// <summary>
    /// Sent by a list box with the LBS_WANTKEYBOARDINPUT style to its owner in response to a WM_CHAR message. 
    /// </summary>
    CHARTOITEM = 0x002F,
    /// <summary>
    /// An application sends a WM_SETFONT message to specify the font that a control is to use when drawing text. 
    /// </summary>
    SETFONT = 0x0030,
    /// <summary>
    /// An application sends a WM_GETFONT message to a control to retrieve the font with which the control is currently drawing its text. 
    /// </summary>
    GETFONT = 0x0031,
    /// <summary>
    /// An application sends a WM_SETHOTKEY message to a window to associate a hot key with the window. When the user presses the hot key, the system activates the window. 
    /// </summary>
    SETHOTKEY = 0x0032,
    /// <summary>
    /// An application sends a WM_GETHOTKEY message to determine the hot key associated with a window. 
    /// </summary>
    GETHOTKEY = 0x0033,
    /// <summary>
    /// The WM_QUERYDRAGICON message is sent to a minimized (iconic) window. The window is about to be dragged by the user but does not have an icon defined for its class. An application can return a handle to an icon or cursor. The system displays this cursor or icon while the user drags the icon.
    /// </summary>
    QUERYDRAGICON = 0x0037,
    /// <summary>
    /// The system sends the WM_COMPAREITEM message to determine the relative position of a new item in the sorted list of an owner-drawn combo box or list box. Whenever the application adds a new item, the system sends this message to the owner of a combo box or list box created with the CBS_SORT or LBS_SORT style. 
    /// </summary>
    COMPAREITEM = 0x0039,
    /// <summary>
    /// Active Accessibility sends the WM_GETOBJECT message to obtain information about an accessible object contained in a server application. 
    /// Applications never send this message directly. It is sent only by Active Accessibility in response to calls to AccessibleObjectFromPoint, AccessibleObjectFromEvent, or AccessibleObjectFromWindow. However, server applications handle this message. 
    /// </summary>
    GETOBJECT = 0x003D,
    /// <summary>
    /// The WM_COMPACTING message is sent to all top-level windows when the system detects more than 12.5 percent of system time over a 30- to 60-second interval is being spent compacting memory. This indicates that system memory is low.
    /// </summary>
    COMPACTING = 0x0041,
    /// <summary>
    /// WM_COMMNOTIFY is Obsolete for Win32-Based Applications
    /// </summary>
    [Obsolete("Obsolete for Win32 Based Applications")]
    COMMNOTIFY = 0x0044,
    /// <summary>
    /// The WM_WINDOWPOSCHANGING message is sent to a window whose size, position, or place in the Z order is about to change as a result of a call to the SetWindowPos function or another window-management function.
    /// </summary>
    WINDOWPOSCHANGING = 0x0046,
    /// <summary>
    /// The WM_WINDOWPOSCHANGED message is sent to a window whose size, position, or place in the Z order has changed as a result of a call to the SetWindowPos function or another window-management function.
    /// </summary>
    WINDOWPOSCHANGED = 0x0047,
    /// <summary>
    /// Notifies applications that the system, typically a battery-powered personal computer, is about to enter a suspended mode.
    /// Use: POWERBROADCAST
    /// </summary>
    [Obsolete("Provided only for compatibility with 16-bit Windows-based applications")]
    POWER = 0x0048,
    /// <summary>
    /// An application sends the WM_COPYDATA message to pass data to another application. 
    /// </summary>
    COPYDATA = 0x004A,
    /// <summary>
    /// The WM_CANCELJOURNAL message is posted to an application when a user cancels the application's journaling activities. The message is posted with a NULL window handle. 
    /// </summary>
    CANCELJOURNAL = 0x004B,
    /// <summary>
    /// Sent by a common control to its parent window when an event has occurred or the control requires some information. 
    /// </summary>
    NOTIFY = 0x004E,
    /// <summary>
    /// The WM_INPUTLANGCHANGEREQUEST message is posted to the window with the focus when the user chooses a new input language, either with the hotkey (specified in the Keyboard control panel application) or from the indicator on the system taskbar. An application can accept the change by passing the message to the DefWindowProc function or reject the change (and prevent it from taking place) by returning immediately. 
    /// </summary>
    INPUTLANGCHANGEREQUEST = 0x0050,
    /// <summary>
    /// The WM_INPUTLANGCHANGE message is sent to the topmost affected window after an application's input language has been changed. You should make any application-specific settings and pass the message to the DefWindowProc function, which passes the message to all first-level child windows. These child windows can pass the message to DefWindowProc to have it pass the message to their child windows, and so on. 
    /// </summary>
    INPUTLANGCHANGE = 0x0051,
    /// <summary>
    /// Sent to an application that has initiated a training card with Microsoft Windows Help. The message informs the application when the user clicks an authorable button. An application initiates a training card by specifying the HELP_TCARD command in a call to the WinHelp function.
    /// </summary>
    TCARD = 0x0052,
    /// <summary>
    /// Indicates that the user pressed the F1 key. If a menu is active when F1 is pressed, WM_HELP is sent to the window associated with the menu; otherwise, WM_HELP is sent to the window that has the keyboard focus. If no window has the keyboard focus, WM_HELP is sent to the currently active window. 
    /// </summary>
    HELP = 0x0053,
    /// <summary>
    /// The WM_USERCHANGED message is sent to all windows after the user has logged on or off. When the user logs on or off, the system updates the user-specific settings. The system sends this message immediately after updating the settings.
    /// </summary>
    USERCHANGED = 0x0054,
    /// <summary>
    /// Determines if a window accepts ANSI or Unicode structures in the WM_NOTIFY notification message. WM_NOTIFYFORMAT messages are sent from a common control to its parent window and from the parent window to the common control.
    /// </summary>
    NOTIFYFORMAT = 0x0055,
    /// <summary>
    /// The WM_CONTEXTMENU message notifies a window that the user clicked the right mouse button (right-clicked) in the window.
    /// </summary>
    CONTEXTMENU = 0x007B,
    /// <summary>
    /// The WM_STYLECHANGING message is sent to a window when the SetWindowLong function is about to change one or more of the window's styles.
    /// </summary>
    STYLECHANGING = 0x007C,
    /// <summary>
    /// The WM_STYLECHANGED message is sent to a window after the SetWindowLong function has changed one or more of the window's styles
    /// </summary>
    STYLECHANGED = 0x007D,
    /// <summary>
    /// The WM_DISPLAYCHANGE message is sent to all windows when the display resolution has changed.
    /// </summary>
    DISPLAYCHANGE = 0x007E,
    /// <summary>
    /// The WM_GETICON message is sent to a window to retrieve a handle to the large or small icon associated with a window. The system displays the large icon in the ALT+TAB dialog, and the small icon in the window caption. 
    /// </summary>
    GETICON = 0x007F,
    /// <summary>
    /// An application sends the WM_SETICON message to associate a new large or small icon with a window. The system displays the large icon in the ALT+TAB dialog box, and the small icon in the window caption. 
    /// </summary>
    SETICON = 0x0080,
    /// <summary>
    /// The WM_NCCREATE message is sent prior to the WM_CREATE message when a window is first created.
    /// </summary>
    NCCREATE = 0x0081,
    /// <summary>
    /// The WM_NCDESTROY message informs a window that its nonclient area is being destroyed. The DestroyWindow function sends the WM_NCDESTROY message to the window following the WM_DESTROY message. WM_DESTROY is used to free the allocated memory object associated with the window. 
    /// The WM_NCDESTROY message is sent after the child windows have been destroyed. In contrast, WM_DESTROY is sent before the child windows are destroyed.
    /// </summary>
    NCDESTROY = 0x0082,
    /// <summary>
    /// The WM_NCCALCSIZE message is sent when the size and position of a window's client area must be calculated. By processing this message, an application can control the content of the window's client area when the size or position of the window changes.
    /// </summary>
    NCCALCSIZE = 0x0083,
    /// <summary>
    /// The WM_NCHITTEST message is sent to a window when the cursor moves, or when a mouse button is pressed or released. If the mouse is not captured, the message is sent to the window beneath the cursor. Otherwise, the message is sent to the window that has captured the mouse.
    /// </summary>
    NCHITTEST = 0x0084,
    /// <summary>
    /// The WM_NCPAINT message is sent to a window when its frame must be painted. 
    /// </summary>
    NCPAINT = 0x0085,
    /// <summary>
    /// The WM_NCACTIVATE message is sent to a window when its nonclient area needs to be changed to indicate an active or inactive state.
    /// </summary>
    NCACTIVATE = 0x0086,
    /// <summary>
    /// The WM_GETDLGCODE message is sent to the window procedure associated with a control. By default, the system handles all keyboard input to the control; the system interprets certain types of keyboard input as dialog box navigation keys. To override this default behavior, the control can respond to the WM_GETDLGCODE message to indicate the types of input it wants to process itself.
    /// </summary>
    GETDLGCODE = 0x0087,
    /// <summary>
    /// The WM_SYNCPAINT message is used to synchronize painting while avoiding linking independent GUI threads.
    /// </summary>
    SYNCPAINT = 0x0088,
    /// <summary>
    /// The WM_NCMOUSEMOVE message is posted to a window when the cursor is moved within the nonclient area of the window. This message is posted to the window that contains the cursor. If a window has captured the mouse, this message is not posted.
    /// </summary>
    NCMOUSEMOVE = 0x00A0,
    /// <summary>
    /// The WM_NCLBUTTONDOWN message is posted when the user presses the left mouse button while the cursor is within the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse, this message is not posted.
    /// </summary>
    NCLBUTTONDOWN = 0x00A1,
    /// <summary>
    /// The WM_NCLBUTTONUP message is posted when the user releases the left mouse button while the cursor is within the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse, this message is not posted.
    /// </summary>
    NCLBUTTONUP = 0x00A2,
    /// <summary>
    /// The WM_NCLBUTTONDBLCLK message is posted when the user double-clicks the left mouse button while the cursor is within the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse, this message is not posted.
    /// </summary>
    NCLBUTTONDBLCLK = 0x00A3,
    /// <summary>
    /// The WM_NCRBUTTONDOWN message is posted when the user presses the right mouse button while the cursor is within the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse, this message is not posted.
    /// </summary>
    NCRBUTTONDOWN = 0x00A4,
    /// <summary>
    /// The WM_NCRBUTTONUP message is posted when the user releases the right mouse button while the cursor is within the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse, this message is not posted.
    /// </summary>
    NCRBUTTONUP = 0x00A5,
    /// <summary>
    /// The WM_NCRBUTTONDBLCLK message is posted when the user double-clicks the right mouse button while the cursor is within the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse, this message is not posted.
    /// </summary>
    NCRBUTTONDBLCLK = 0x00A6,
    /// <summary>
    /// The WM_NCMBUTTONDOWN message is posted when the user presses the middle mouse button while the cursor is within the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse, this message is not posted.
    /// </summary>
    NCMBUTTONDOWN = 0x00A7,
    /// <summary>
    /// The WM_NCMBUTTONUP message is posted when the user releases the middle mouse button while the cursor is within the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse, this message is not posted.
    /// </summary>
    NCMBUTTONUP = 0x00A8,
    /// <summary>
    /// The WM_NCMBUTTONDBLCLK message is posted when the user double-clicks the middle mouse button while the cursor is within the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse, this message is not posted.
    /// </summary>
    NCMBUTTONDBLCLK = 0x00A9,
    /// <summary>
    /// The WM_NCXBUTTONDOWN message is posted when the user presses the first or second X button while the cursor is in the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse, this message is not posted.
    /// </summary>
    NCXBUTTONDOWN = 0x00AB,
    /// <summary>
    /// The WM_NCXBUTTONUP message is posted when the user releases the first or second X button while the cursor is in the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse, this message is not posted.
    /// </summary>
    NCXBUTTONUP = 0x00AC,
    /// <summary>
    /// The WM_NCXBUTTONDBLCLK message is posted when the user double-clicks the first or second X button while the cursor is in the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse, this message is not posted.
    /// </summary>
    NCXBUTTONDBLCLK = 0x00AD,
    /// <summary>
    /// The WM_INPUT_DEVICE_CHANGE message is sent to the window that registered to receive raw input. A window receives this message through its WindowProc function.
    /// </summary>
    INPUT_DEVICE_CHANGE = 0x00FE,
    /// <summary>
    /// The WM_INPUT message is sent to the window that is getting raw input. 
    /// </summary>
    INPUT = 0x00FF,
    /// <summary>
    /// This message filters for keyboard messages.
    /// </summary>
    KEYFIRST = 0x0100,
    /// <summary>
    /// The WM_KEYDOWN message is posted to the window with the keyboard focus when a nonsystem key is pressed. A nonsystem key is a key that is pressed when the ALT key is not pressed. 
    /// </summary>
    KEYDOWN = 0x0100,
    /// <summary>
    /// The WM_KEYUP message is posted to the window with the keyboard focus when a nonsystem key is released. A nonsystem key is a key that is pressed when the ALT key is not pressed, or a keyboard key that is pressed when a window has the keyboard focus. 
    /// </summary>
    KEYUP = 0x0101,
    /// <summary>
    /// The WM_CHAR message is posted to the window with the keyboard focus when a WM_KEYDOWN message is translated by the TranslateMessage function. The WM_CHAR message contains the character code of the key that was pressed. 
    /// </summary>
    CHAR = 0x0102,
    /// <summary>
    /// The WM_DEADCHAR message is posted to the window with the keyboard focus when a WM_KEYUP message is translated by the TranslateMessage function. WM_DEADCHAR specifies a character code generated by a dead key. A dead key is a key that generates a character, such as the umlaut (double-dot), that is combined with another character to form a composite character. For example, the umlaut-O character (Ö) is generated by typing the dead key for the umlaut character, and then typing the O key. 
    /// </summary>
    DEADCHAR = 0x0103,
    /// <summary>
    /// The WM_SYSKEYDOWN message is posted to the window with the keyboard focus when the user presses the F10 key (which activates the menu bar) or holds down the ALT key and then presses another key. It also occurs when no window currently has the keyboard focus; in this case, the WM_SYSKEYDOWN message is sent to the active window. The window that receives the message can distinguish between these two contexts by checking the context code in the lParam parameter. 
    /// </summary>
    SYSKEYDOWN = 0x0104,
    /// <summary>
    /// The WM_SYSKEYUP message is posted to the window with the keyboard focus when the user releases a key that was pressed while the ALT key was held down. It also occurs when no window currently has the keyboard focus; in this case, the WM_SYSKEYUP message is sent to the active window. The window that receives the message can distinguish between these two contexts by checking the context code in the lParam parameter. 
    /// </summary>
    SYSKEYUP = 0x0105,
    /// <summary>
    /// The WM_SYSCHAR message is posted to the window with the keyboard focus when a WM_SYSKEYDOWN message is translated by the TranslateMessage function. It specifies the character code of a system character key — that is, a character key that is pressed while the ALT key is down. 
    /// </summary>
    SYSCHAR = 0x0106,
    /// <summary>
    /// The WM_SYSDEADCHAR message is sent to the window with the keyboard focus when a WM_SYSKEYDOWN message is translated by the TranslateMessage function. WM_SYSDEADCHAR specifies the character code of a system dead key — that is, a dead key that is pressed while holding down the ALT key. 
    /// </summary>
    SYSDEADCHAR = 0x0107,
    /// <summary>
    /// The WM_UNICHAR message is posted to the window with the keyboard focus when a WM_KEYDOWN message is translated by the TranslateMessage function. The WM_UNICHAR message contains the character code of the key that was pressed. 
    /// The WM_UNICHAR message is equivalent to WM_CHAR, but it uses Unicode Transformation Format (UTF)-32, whereas WM_CHAR uses UTF-16. It is designed to send or post Unicode characters to ANSI windows and it can can handle Unicode Supplementary Plane characters.
    /// </summary>
    UNICHAR = 0x0109,
    /// <summary>
    /// This message filters for keyboard messages.
    /// </summary>
    KEYLAST = 0x0108,
    /// <summary>
    /// Sent immediately before the IME generates the composition string as a result of a keystroke. A window receives this message through its WindowProc function. 
    /// </summary>
    IME_STARTCOMPOSITION = 0x010D,
    /// <summary>
    /// Sent to an application when the IME ends composition. A window receives this message through its WindowProc function. 
    /// </summary>
    IME_ENDCOMPOSITION = 0x010E,
    /// <summary>
    /// Sent to an application when the IME changes composition status as a result of a keystroke. A window receives this message through its WindowProc function. 
    /// </summary>
    IME_COMPOSITION = 0x010F,
    IME_KEYLAST = 0x010F,
    /// <summary>
    /// The WM_INITDIALOG message is sent to the dialog box procedure immediately before a dialog box is displayed. Dialog box procedures typically use this message to initialize controls and carry out any other initialization tasks that affect the appearance of the dialog box. 
    /// </summary>
    INITDIALOG = 0x0110,
    /// <summary>
    /// The WM_COMMAND message is sent when the user selects a command item from a menu, when a control sends a notification message to its parent window, or when an accelerator keystroke is translated. 
    /// </summary>
    COMMAND = 0x0111,
    /// <summary>
    /// A window receives this message when the user chooses a command from the Window menu, clicks the maximize button, minimize button, restore button, close button, or moves the form. You can stop the form from moving by filtering this out.
    /// </summary>
    SYSCOMMAND = 0x0112,
    /// <summary>
    /// The WM_TIMER message is posted to the installing thread's message queue when a timer expires. The message is posted by the GetMessage or PeekMessage function. 
    /// </summary>
    TIMER = 0x0113,
    /// <summary>
    /// The WM_HSCROLL message is sent to a window when a scroll event occurs in the window's standard horizontal scroll bar. This message is also sent to the owner of a horizontal scroll bar control when a scroll event occurs in the control. 
    /// </summary>
    HSCROLL = 0x0114,
    /// <summary>
    /// The WM_VSCROLL message is sent to a window when a scroll event occurs in the window's standard vertical scroll bar. This message is also sent to the owner of a vertical scroll bar control when a scroll event occurs in the control. 
    /// </summary>
    VSCROLL = 0x0115,
    /// <summary>
    /// The WM_INITMENU message is sent when a menu is about to become active. It occurs when the user clicks an item on the menu bar or presses a menu key. This allows the application to modify the menu before it is displayed. 
    /// </summary>
    INITMENU = 0x0116,
    /// <summary>
    /// The WM_INITMENUPOPUP message is sent when a drop-down menu or submenu is about to become active. This allows an application to modify the menu before it is displayed, without changing the entire menu. 
    /// </summary>
    INITMENUPOPUP = 0x0117,
    /// <summary>
    /// The WM_MENUSELECT message is sent to a menu's owner window when the user selects a menu item. 
    /// </summary>
    MENUSELECT = 0x011F,
    /// <summary>
    /// The WM_MENUCHAR message is sent when a menu is active and the user presses a key that does not correspond to any mnemonic or accelerator key. This message is sent to the window that owns the menu. 
    /// </summary>
    MENUCHAR = 0x0120,
    /// <summary>
    /// The WM_ENTERIDLE message is sent to the owner window of a modal dialog box or menu that is entering an idle state. A modal dialog box or menu enters an idle state when no messages are waiting in its queue after it has processed one or more previous messages. 
    /// </summary>
    ENTERIDLE = 0x0121,
    /// <summary>
    /// The WM_MENURBUTTONUP message is sent when the user releases the right mouse button while the cursor is on a menu item. 
    /// </summary>
    MENURBUTTONUP = 0x0122,
    /// <summary>
    /// The WM_MENUDRAG message is sent to the owner of a drag-and-drop menu when the user drags a menu item. 
    /// </summary>
    MENUDRAG = 0x0123,
    /// <summary>
    /// The WM_MENUGETOBJECT message is sent to the owner of a drag-and-drop menu when the mouse cursor enters a menu item or moves from the center of the item to the top or bottom of the item. 
    /// </summary>
    MENUGETOBJECT = 0x0124,
    /// <summary>
    /// The WM_UNINITMENUPOPUP message is sent when a drop-down menu or submenu has been destroyed. 
    /// </summary>
    UNINITMENUPOPUP = 0x0125,
    /// <summary>
    /// The WM_MENUCOMMAND message is sent when the user makes a selection from a menu. 
    /// </summary>
    MENUCOMMAND = 0x0126,
    /// <summary>
    /// An application sends the WM_CHANGEUISTATE message to indicate that the user interface (UI) state should be changed.
    /// </summary>
    CHANGEUISTATE = 0x0127,
    /// <summary>
    /// An application sends the WM_UPDATEUISTATE message to change the user interface (UI) state for the specified window and all its child windows.
    /// </summary>
    UPDATEUISTATE = 0x0128,
    /// <summary>
    /// An application sends the WM_QUERYUISTATE message to retrieve the user interface (UI) state for a window.
    /// </summary>
    QUERYUISTATE = 0x0129,
    /// <summary>
    /// The WM_CTLCOLORMSGBOX message is sent to the owner window of a message box before Windows draws the message box. By responding to this message, the owner window can set the text and background colors of the message box by using the given display device context handle. 
    /// </summary>
    CTLCOLORMSGBOX = 0x0132,
    /// <summary>
    /// An edit control that is not read-only or disabled sends the WM_CTLCOLOREDIT message to its parent window when the control is about to be drawn. By responding to this message, the parent window can use the specified device context handle to set the text and background colors of the edit control. 
    /// </summary>
    CTLCOLOREDIT = 0x0133,
    /// <summary>
    /// Sent to the parent window of a list box before the system draws the list box. By responding to this message, the parent window can set the text and background colors of the list box by using the specified display device context handle. 
    /// </summary>
    CTLCOLORLISTBOX = 0x0134,
    /// <summary>
    /// The WM_CTLCOLORBTN message is sent to the parent window of a button before drawing the button. The parent window can change the button's text and background colors. However, only owner-drawn buttons respond to the parent window processing this message. 
    /// </summary>
    CTLCOLORBTN = 0x0135,
    /// <summary>
    /// The WM_CTLCOLORDLG message is sent to a dialog box before the system draws the dialog box. By responding to this message, the dialog box can set its text and background colors using the specified display device context handle. 
    /// </summary>
    CTLCOLORDLG = 0x0136,
    /// <summary>
    /// The WM_CTLCOLORSCROLLBAR message is sent to the parent window of a scroll bar control when the control is about to be drawn. By responding to this message, the parent window can use the display context handle to set the background color of the scroll bar control. 
    /// </summary>
    CTLCOLORSCROLLBAR = 0x0137,
    /// <summary>
    /// A static control, or an edit control that is read-only or disabled, sends the WM_CTLCOLORSTATIC message to its parent window when the control is about to be drawn. By responding to this message, the parent window can use the specified device context handle to set the text and background colors of the static control. 
    /// </summary>
    CTLCOLORSTATIC = 0x0138,
    /// <summary>
    /// Use WM_MOUSEFIRST to specify the first mouse message. Use the PeekMessage() Function.
    /// </summary>
    MOUSEFIRST = 0x0200,
    /// <summary>
    /// The WM_MOUSEMOVE message is posted to a window when the cursor moves. If the mouse is not captured, the message is posted to the window that contains the cursor. Otherwise, the message is posted to the window that has captured the mouse.
    /// </summary>
    MOUSEMOVE = 0x0200,
    /// <summary>
    /// The WM_LBUTTONDOWN message is posted when the user presses the left mouse button while the cursor is in the client area of a window. If the mouse is not captured, the message is posted to the window beneath the cursor. Otherwise, the message is posted to the window that has captured the mouse.
    /// </summary>
    LBUTTONDOWN = 0x0201,
    /// <summary>
    /// The WM_LBUTTONUP message is posted when the user releases the left mouse button while the cursor is in the client area of a window. If the mouse is not captured, the message is posted to the window beneath the cursor. Otherwise, the message is posted to the window that has captured the mouse.
    /// </summary>
    LBUTTONUP = 0x0202,
    /// <summary>
    /// The WM_LBUTTONDBLCLK message is posted when the user double-clicks the left mouse button while the cursor is in the client area of a window. If the mouse is not captured, the message is posted to the window beneath the cursor. Otherwise, the message is posted to the window that has captured the mouse.
    /// </summary>
    LBUTTONDBLCLK = 0x0203,
    /// <summary>
    /// The WM_RBUTTONDOWN message is posted when the user presses the right mouse button while the cursor is in the client area of a window. If the mouse is not captured, the message is posted to the window beneath the cursor. Otherwise, the message is posted to the window that has captured the mouse.
    /// </summary>
    RBUTTONDOWN = 0x0204,
    /// <summary>
    /// The WM_RBUTTONUP message is posted when the user releases the right mouse button while the cursor is in the client area of a window. If the mouse is not captured, the message is posted to the window beneath the cursor. Otherwise, the message is posted to the window that has captured the mouse.
    /// </summary>
    RBUTTONUP = 0x0205,
    /// <summary>
    /// The WM_RBUTTONDBLCLK message is posted when the user double-clicks the right mouse button while the cursor is in the client area of a window. If the mouse is not captured, the message is posted to the window beneath the cursor. Otherwise, the message is posted to the window that has captured the mouse.
    /// </summary>
    RBUTTONDBLCLK = 0x0206,
    /// <summary>
    /// The WM_MBUTTONDOWN message is posted when the user presses the middle mouse button while the cursor is in the client area of a window. If the mouse is not captured, the message is posted to the window beneath the cursor. Otherwise, the message is posted to the window that has captured the mouse.
    /// </summary>
    MBUTTONDOWN = 0x0207,
    /// <summary>
    /// The WM_MBUTTONUP message is posted when the user releases the middle mouse button while the cursor is in the client area of a window. If the mouse is not captured, the message is posted to the window beneath the cursor. Otherwise, the message is posted to the window that has captured the mouse.
    /// </summary>
    MBUTTONUP = 0x0208,
    /// <summary>
    /// The WM_MBUTTONDBLCLK message is posted when the user double-clicks the middle mouse button while the cursor is in the client area of a window. If the mouse is not captured, the message is posted to the window beneath the cursor. Otherwise, the message is posted to the window that has captured the mouse.
    /// </summary>
    MBUTTONDBLCLK = 0x0209,
    /// <summary>
    /// The WM_MOUSEWHEEL message is sent to the focus window when the mouse wheel is rotated. The DefWindowProc function propagates the message to the window's parent. There should be no internal forwarding of the message, since DefWindowProc propagates it up the parent chain until it finds a window that processes it.
    /// </summary>
    MOUSEWHEEL = 0x020A,
    /// <summary>
    /// The WM_XBUTTONDOWN message is posted when the user presses the first or second X button while the cursor is in the client area of a window. If the mouse is not captured, the message is posted to the window beneath the cursor. Otherwise, the message is posted to the window that has captured the mouse. 
   /// </summary>
    XBUTTONDOWN = 0x020B,
    /// <summary>
    /// The WM_XBUTTONUP message is posted when the user releases the first or second X button while the cursor is in the client area of a window. If the mouse is not captured, the message is posted to the window beneath the cursor. Otherwise, the message is posted to the window that has captured the mouse.
    /// </summary>
    XBUTTONUP = 0x020C,
    /// <summary>
    /// The WM_XBUTTONDBLCLK message is posted when the user double-clicks the first or second X button while the cursor is in the client area of a window. If the mouse is not captured, the message is posted to the window beneath the cursor. Otherwise, the message is posted to the window that has captured the mouse.
    /// </summary>
    XBUTTONDBLCLK = 0x020D,
    /// <summary>
    /// The WM_MOUSEHWHEEL message is sent to the focus window when the mouse's horizontal scroll wheel is tilted or rotated. The DefWindowProc function propagates the message to the window's parent. There should be no internal forwarding of the message, since DefWindowProc propagates it up the parent chain until it finds a window that processes it.
    /// </summary>
    MOUSEHWHEEL = 0x020E,
    /// <summary>
    /// Use WM_MOUSELAST to specify the last mouse message. Used with PeekMessage() Function.
    /// </summary>
    MOUSELAST = 0x020E,
    /// <summary>
    /// The WM_PARENTNOTIFY message is sent to the parent of a child window when the child window is created or destroyed, or when the user clicks a mouse button while the cursor is over the child window. When the child window is being created, the system sends WM_PARENTNOTIFY just before the CreateWindow or CreateWindowEx function that creates the window returns. When the child window is being destroyed, the system sends the message before any processing to destroy the window takes place.
    /// </summary>
    PARENTNOTIFY = 0x0210,
    /// <summary>
    /// The WM_ENTERMENULOOP message informs an application's main window procedure that a menu modal loop has been entered. 
    /// </summary>
    ENTERMENULOOP = 0x0211,
    /// <summary>
    /// The WM_EXITMENULOOP message informs an application's main window procedure that a menu modal loop has been exited. 
    /// </summary>
    EXITMENULOOP = 0x0212,
    /// <summary>
    /// The WM_NEXTMENU message is sent to an application when the right or left arrow key is used to switch between the menu bar and the system menu. 
    /// </summary>
    NEXTMENU = 0x0213,
    /// <summary>
    /// The WM_SIZING message is sent to a window that the user is resizing. By processing this message, an application can monitor the size and position of the drag rectangle and, if needed, change its size or position. 
    /// </summary>
    SIZING = 0x0214,
    /// <summary>
    /// The WM_CAPTURECHANGED message is sent to the window that is losing the mouse capture.
    /// </summary>
    CAPTURECHANGED = 0x0215,
    /// <summary>
    /// The WM_MOVING message is sent to a window that the user is moving. By processing this message, an application can monitor the position of the drag rectangle and, if needed, change its position.
    /// </summary>
    MOVING = 0x0216,
    /// <summary>
    /// Notifies applications that a power-management event has occurred.
    /// </summary>
    POWERBROADCAST = 0x0218,
    /// <summary>
    /// Notifies an application of a change to the hardware configuration of a device or the computer.
    /// </summary>
    DEVICECHANGE = 0x0219,
    /// <summary>
    /// An application sends the WM_MDICREATE message to a multiple-document interface (MDI) client window to create an MDI child window. 
    /// </summary>
    MDICREATE = 0x0220,
    /// <summary>
    /// An application sends the WM_MDIDESTROY message to a multiple-document interface (MDI) client window to close an MDI child window. 
    /// </summary>
    MDIDESTROY = 0x0221,
    /// <summary>
    /// An application sends the WM_MDIACTIVATE message to a multiple-document interface (MDI) client window to instruct the client window to activate a different MDI child window. 
    /// </summary>
    MDIACTIVATE = 0x0222,
    /// <summary>
    /// An application sends the WM_MDIRESTORE message to a multiple-document interface (MDI) client window to restore an MDI child window from maximized or minimized size. 
    /// </summary>
    MDIRESTORE = 0x0223,
    /// <summary>
    /// An application sends the WM_MDINEXT message to a multiple-document interface (MDI) client window to activate the next or previous child window. 
    /// </summary>
    MDINEXT = 0x0224,
    /// <summary>
    /// An application sends the WM_MDIMAXIMIZE message to a multiple-document interface (MDI) client window to maximize an MDI child window. The system resizes the child window to make its client area fill the client window. The system places the child window's window menu icon in the rightmost position of the frame window's menu bar, and places the child window's restore icon in the leftmost position. The system also appends the title bar text of the child window to that of the frame window. 
    /// </summary>
    MDIMAXIMIZE = 0x0225,
    /// <summary>
    /// An application sends the WM_MDITILE message to a multiple-document interface (MDI) client window to arrange all of its MDI child windows in a tile format. 
    /// </summary>
    MDITILE = 0x0226,
    /// <summary>
    /// An application sends the WM_MDICASCADE message to a multiple-document interface (MDI) client window to arrange all its child windows in a cascade format. 
    /// </summary>
    MDICASCADE = 0x0227,
    /// <summary>
    /// An application sends the WM_MDIICONARRANGE message to a multiple-document interface (MDI) client window to arrange all minimized MDI child windows. It does not affect child windows that are not minimized. 
    /// </summary>
    MDIICONARRANGE = 0x0228,
    /// <summary>
    /// An application sends the WM_MDIGETACTIVE message to a multiple-document interface (MDI) client window to retrieve the handle to the active MDI child window. 
    /// </summary>
    MDIGETACTIVE = 0x0229,
    /// <summary>
    /// An application sends the WM_MDISETMENU message to a multiple-document interface (MDI) client window to replace the entire menu of an MDI frame window, to replace the window menu of the frame window, or both. 
    /// </summary>
    MDISETMENU = 0x0230,
    /// <summary>
    /// The WM_ENTERSIZEMOVE message is sent one time to a window after it enters the moving or sizing modal loop. The window enters the moving or sizing modal loop when the user clicks the window's title bar or sizing border, or when the window passes the WM_SYSCOMMAND message to the DefWindowProc function and the wParam parameter of the message specifies the SC_MOVE or SC_SIZE value. The operation is complete when DefWindowProc returns. 
    /// The system sends the WM_ENTERSIZEMOVE message regardless of whether the dragging of full windows is enabled.
    /// </summary>
    ENTERSIZEMOVE = 0x0231,
    /// <summary>
    /// The WM_EXITSIZEMOVE message is sent one time to a window, after it has exited the moving or sizing modal loop. The window enters the moving or sizing modal loop when the user clicks the window's title bar or sizing border, or when the window passes the WM_SYSCOMMAND message to the DefWindowProc function and the wParam parameter of the message specifies the SC_MOVE or SC_SIZE value. The operation is complete when DefWindowProc returns. 
    /// </summary>
    EXITSIZEMOVE = 0x0232,
    /// <summary>
    /// Sent when the user drops a file on the window of an application that has registered itself as a recipient of dropped files.
    /// </summary>
    DROPFILES = 0x0233,
    /// <summary>
    /// An application sends the WM_MDIREFRESHMENU message to a multiple-document interface (MDI) client window to refresh the window menu of the MDI frame window. 
    /// </summary>
    MDIREFRESHMENU = 0x0234,
    /// <summary>
    /// Sent to an application when a window is activated. A window receives this message through its WindowProc function. 
    /// </summary>
    IME_SETCONTEXT = 0x0281,
    /// <summary>
    /// Sent to an application to notify it of changes to the IME window. A window receives this message through its WindowProc function. 
    /// </summary>
    IME_NOTIFY = 0x0282,
    /// <summary>
    /// Sent by an application to direct the IME window to carry out the requested command. The application uses this message to control the IME window that it has created. To send this message, the application calls the SendMessage function with the following parameters.
    /// </summary>
    IME_CONTROL = 0x0283,
    /// <summary>
    /// Sent to an application when the IME window finds no space to extend the area for the composition window. A window receives this message through its WindowProc function. 
    /// </summary>
    IME_COMPOSITIONFULL = 0x0284,
    /// <summary>
    /// Sent to an application when the operating system is about to change the current IME. A window receives this message through its WindowProc function. 
    /// </summary>
    IME_SELECT = 0x0285,
    /// <summary>
    /// Sent to an application when the IME gets a character of the conversion result. A window receives this message through its WindowProc function. 
    /// </summary>
    IME_CHAR = 0x0286,
    /// <summary>
    /// Sent to an application to provide commands and request information. A window receives this message through its WindowProc function. 
    /// </summary>
    IME_REQUEST = 0x0288,
    /// <summary>
    /// Sent to an application by the IME to notify the application of a key press and to keep message order. A window receives this message through its WindowProc function. 
    /// </summary>
    IME_KEYDOWN = 0x0290,
    /// <summary>
    /// Sent to an application by the IME to notify the application of a key release and to keep message order. A window receives this message through its WindowProc function. 
    /// </summary>
    IME_KEYUP = 0x0291,
    /// <summary>
    /// The WM_MOUSEHOVER message is posted to a window when the cursor hovers over the client area of the window for the period of time specified in a prior call to TrackMouseEvent.
    /// </summary>
    MOUSEHOVER = 0x02A1,
    /// <summary>
    /// The WM_MOUSELEAVE message is posted to a window when the cursor leaves the client area of the window specified in a prior call to TrackMouseEvent.
    /// </summary>
    MOUSELEAVE = 0x02A3,
    /// <summary>
    /// The WM_NCMOUSEHOVER message is posted to a window when the cursor hovers over the nonclient area of the window for the period of time specified in a prior call to TrackMouseEvent.
    /// </summary>
    NCMOUSEHOVER = 0x02A0,
    /// <summary>
    /// The WM_NCMOUSELEAVE message is posted to a window when the cursor leaves the nonclient area of the window specified in a prior call to TrackMouseEvent.
    /// </summary>
    NCMOUSELEAVE = 0x02A2,
    /// <summary>
    /// The WM_WTSSESSION_CHANGE message notifies applications of changes in session state.
    /// </summary>
    WTSSESSION_CHANGE = 0x02B1,
    TABLET_FIRST = 0x02c0,
    TABLET_LAST = 0x02df,
    /// <summary>
    /// An application sends a WM_CUT message to an edit control or combo box to delete (cut) the current selection, if any, in the edit control and copy the deleted text to the clipboard in CF_TEXT format. 
    /// </summary>
    CUT = 0x0300,
    /// <summary>
    /// An application sends the WM_COPY message to an edit control or combo box to copy the current selection to the clipboard in CF_TEXT format. 
    /// </summary>
    COPY = 0x0301,
    /// <summary>
    /// An application sends a WM_PASTE message to an edit control or combo box to copy the current content of the clipboard to the edit control at the current caret position. Data is inserted only if the clipboard contains data in CF_TEXT format. 
    /// </summary>
    PASTE = 0x0302,
    /// <summary>
    /// An application sends a WM_CLEAR message to an edit control or combo box to delete (clear) the current selection, if any, from the edit control. 
    /// </summary>
    CLEAR = 0x0303,
    /// <summary>
    /// An application sends a WM_UNDO message to an edit control to undo the last operation. When this message is sent to an edit control, the previously deleted text is restored or the previously added text is deleted.
    /// </summary>
    UNDO = 0x0304,
    /// <summary>
    /// The WM_RENDERFORMAT message is sent to the clipboard owner if it has delayed rendering a specific clipboard format and if an application has requested data in that format. The clipboard owner must render data in the specified format and place it on the clipboard by calling the SetClipboardData function. 
    /// </summary>
    RENDERFORMAT = 0x0305,
    /// <summary>
    /// The WM_RENDERALLFORMATS message is sent to the clipboard owner before it is destroyed, if the clipboard owner has delayed rendering one or more clipboard formats. For the content of the clipboard to remain available to other applications, the clipboard owner must render data in all the formats it is capable of generating, and place the data on the clipboard by calling the SetClipboardData function. 
    /// </summary>
    RENDERALLFORMATS = 0x0306,
    /// <summary>
    /// The WM_DESTROYCLIPBOARD message is sent to the clipboard owner when a call to the EmptyClipboard function empties the clipboard. 
    /// </summary>
    DESTROYCLIPBOARD = 0x0307,
    /// <summary>
    /// The WM_DRAWCLIPBOARD message is sent to the first window in the clipboard viewer chain when the content of the clipboard changes. This enables a clipboard viewer window to display the new content of the clipboard. 
    /// </summary>
    DRAWCLIPBOARD = 0x0308,
    /// <summary>
    /// The WM_PAINTCLIPBOARD message is sent to the clipboard owner by a clipboard viewer window when the clipboard contains data in the CF_OWNERDISPLAY format and the clipboard viewer's client area needs repainting. 
    /// </summary>
    PAINTCLIPBOARD = 0x0309,
    /// <summary>
    /// The WM_VSCROLLCLIPBOARD message is sent to the clipboard owner by a clipboard viewer window when the clipboard contains data in the CF_OWNERDISPLAY format and an event occurs in the clipboard viewer's vertical scroll bar. The owner should scroll the clipboard image and update the scroll bar values. 
    /// </summary>
    VSCROLLCLIPBOARD = 0x030A,
    /// <summary>
    /// The WM_SIZECLIPBOARD message is sent to the clipboard owner by a clipboard viewer window when the clipboard contains data in the CF_OWNERDISPLAY format and the clipboard viewer's client area has changed size. 
    /// </summary>
    SIZECLIPBOARD = 0x030B,
    /// <summary>
    /// The WM_ASKCBFORMATNAME message is sent to the clipboard owner by a clipboard viewer window to request the name of a CF_OWNERDISPLAY clipboard format.
    /// </summary>
    ASKCBFORMATNAME = 0x030C,
    /// <summary>
    /// The WM_CHANGECBCHAIN message is sent to the first window in the clipboard viewer chain when a window is being removed from the chain. 
    /// </summary>
    CHANGECBCHAIN = 0x030D,
    /// <summary>
    /// The WM_HSCROLLCLIPBOARD message is sent to the clipboard owner by a clipboard viewer window. This occurs when the clipboard contains data in the CF_OWNERDISPLAY format and an event occurs in the clipboard viewer's horizontal scroll bar. The owner should scroll the clipboard image and update the scroll bar values. 
    /// </summary>
    HSCROLLCLIPBOARD = 0x030E,
    /// <summary>
    /// This message informs a window that it is about to receive the keyboard focus, giving the window the opportunity to realize its logical palette when it receives the focus. 
    /// </summary>
    QUERYNEWPALETTE = 0x030F,
    /// <summary>
    /// The WM_PALETTEISCHANGING message informs applications that an application is going to realize its logical palette. 
    /// </summary>
    PALETTEISCHANGING = 0x0310,
    /// <summary>
    /// This message is sent by the OS to all top-level and overlapped windows after the window with the keyboard focus realizes its logical palette. 
    /// This message enables windows that do not have the keyboard focus to realize their logical palettes and update their client areas.
    /// </summary>
    PALETTECHANGED = 0x0311,
    /// <summary>
    /// The WM_HOTKEY message is posted when the user presses a hot key registered by the RegisterHotKey function. The message is placed at the top of the message queue associated with the thread that registered the hot key. 
    /// </summary>
    HOTKEY = 0x0312,
    /// <summary>
    /// The WM_PRINT message is sent to a window to request that it draw itself in the specified device context, most commonly in a printer device context.
    /// </summary>
    PRINT = 0x0317,
    /// <summary>
    /// The WM_PRINTCLIENT message is sent to a window to request that it draw its client area in the specified device context, most commonly in a printer device context.
    /// </summary>
    PRINTCLIENT = 0x0318,
    /// <summary>
    /// The WM_APPCOMMAND message notifies a window that the user generated an application command event, for example, by clicking an application command button using the mouse or typing an application command key on the keyboard.
    /// </summary>
    APPCOMMAND = 0x0319,
    /// <summary>
    /// The WM_THEMECHANGED message is broadcast to every window following a theme change event. Examples of theme change events are the activation of a theme, the deactivation of a theme, or a transition from one theme to another.
    /// </summary>
    THEMECHANGED = 0x031A,
    /// <summary>
    /// Sent when the contents of the clipboard have changed.
    /// </summary>
    CLIPBOARDUPDATE = 0x031D,
    /// <summary>
    /// The system will send a window the WM_DWMCOMPOSITIONCHANGED message to indicate that the availability of desktop composition has changed.
    /// </summary>
    DWMCOMPOSITIONCHANGED = 0x031E,
    /// <summary>
    /// WM_DWMNCRENDERINGCHANGED is called when the non-client area rendering status of a window has changed. Only windows that have set the flag DWM_BLURBEHIND.fTransitionOnMaximized to true will get this message. 
    /// </summary>
    DWMNCRENDERINGCHANGED = 0x031F,
    /// <summary>
    /// Sent to all top-level windows when the colorization color has changed. 
    /// </summary>
    DWMCOLORIZATIONCOLORCHANGED = 0x0320,
    /// <summary>
    /// WM_DWMWINDOWMAXIMIZEDCHANGE will let you know when a DWM composed window is maximized. You also have to register for this message as well. You'd have other windowd go opaque when this message is sent.
    /// </summary>
    DWMWINDOWMAXIMIZEDCHANGE = 0x0321,
    /// <summary>
    /// Sent to request extended title bar information. A window receives this message through its WindowProc function.
    /// </summary>
    GETTITLEBARINFOEX = 0x033F,
    HANDHELDFIRST = 0x0358,
    HANDHELDLAST = 0x035F,
    AFXFIRST = 0x0360,
    AFXLAST = 0x037F,
    PENWINFIRST = 0x0380,
    PENWINLAST = 0x038F,
    /// <summary>
    /// The WM_APP constant is used by applications to help define private messages, usually of the form WM_APP+X, where X is an integer value. 
    /// </summary>
    APP = 0x8000,
    /// <summary>
    /// The WM_USER constant is used by applications to help define private messages for use by private window classes, usually of the form WM_USER+X, where X is an integer value. 
    /// </summary>
    USER = 0x0400,

    /// <summary>
    /// An application sends the WM_CPL_LAUNCH message to Windows Control Panel to request that a Control Panel application be started. 
    /// </summary>
    CPL_LAUNCH = USER+0x1000,
    /// <summary>
    /// The WM_CPL_LAUNCHED message is sent when a Control Panel application, started by the WM_CPL_LAUNCH message, has closed. The WM_CPL_LAUNCHED message is sent to the window identified by the wParam parameter of the WM_CPL_LAUNCH message that started the application. 
    /// </summary>
    CPL_LAUNCHED = USER+0x1001,
    /// <summary>
    /// WM_SYSTIMER is a well-known yet still undocumented message. Windows uses WM_SYSTIMER for internal actions like scrolling.
    /// </summary>
    SYSTIMER = 0x118,

    /// <summary>
    /// The accessibility state has changed.
    /// </summary>
    HSHELL_ACCESSIBILITYSTATE = 11,
    /// <summary>
    /// The shell should activate its main window.
    /// </summary>
    HSHELL_ACTIVATESHELLWINDOW = 3,
    /// <summary>
    /// The user completed an input event (for example, pressed an application command button on the mouse or an application command key on the keyboard), and the application did not handle the WM_APPCOMMAND message generated by that input.
    /// If the Shell procedure handles the WM_COMMAND message, it should not call CallNextHookEx. See the Return Value section for more information.
    /// </summary>
    HSHELL_APPCOMMAND = 12,
    /// <summary>
    /// A window is being minimized or maximized. The system needs the coordinates of the minimized rectangle for the window.
    /// </summary>
    HSHELL_GETMINRECT = 5,
    /// <summary>
    /// Keyboard language was changed or a new keyboard layout was loaded.
    /// </summary>
    HSHELL_LANGUAGE = 8,
    /// <summary>
    /// The title of a window in the task bar has been redrawn.
    /// </summary>
    HSHELL_REDRAW = 6,
    /// <summary>
    /// The user has selected the task list. A shell application that provides a task list should return TRUE to prevent Windows from starting its task list.
    /// </summary>
    HSHELL_TASKMAN = 7,
    /// <summary>
    /// A top-level, unowned window has been created. The window exists when the system calls this hook.
    /// </summary>
    HSHELL_WINDOWCREATED = 1,
    /// <summary>
    /// A top-level, unowned window is about to be destroyed. The window still exists when the system calls this hook.
    /// </summary>
    HSHELL_WINDOWDESTROYED = 2,
    /// <summary>
    /// The activation has changed to a different top-level, unowned window.
    /// </summary>
    HSHELL_WINDOWACTIVATED = 4,
    /// <summary>
    /// A top-level window is being replaced. The window exists when the system calls this hook.
    /// </summary>
    HSHELL_WINDOWREPLACED = 13
}
```

## VB Definition:
```cs
Public Enum WindowsMessages As UInteger
    ''' <summary>
    '''The WM_ACTIVATE message is sent when a window is being activated or deactivated. This message is sent first to the window procedure of the top-level window being deactivated; it is then sent to the window procedure of the top-level window being activated.
    ''' </summary>
    ''' <remarks></remarks>
    WM_ACTIVATE = &H6

    ''' <summary>
    '''The WM_ACTIVATEAPP message is sent when a window belonging to a different application than the active window is about to be activated. The message is sent to the application whose window is being activated and to the application whose window is being deactivated.
    ''' </summary>
    ''' <remarks></remarks>
    WM_ACTIVATEAPP = &H1C

    ''' <summary>
    '''Definition Needed
    ''' </summary>
    ''' <remarks></remarks>
    WM_AFXFIRST = &H360

    ''' <summary>
    '''Definition Needed
    ''' </summary>
    ''' <remarks></remarks>
    WM_AFXLAST = &H37F

    ''' <summary>
    '''The WM_APP constant is used by applications to help define private messages usually of the form WM_APP+X where X is an integer value.
    ''' </summary>
    ''' <remarks></remarks>
    WM_APP = &H8000

    ''' <summary>
    '''The WM_ASKCBFORMATNAME message is sent to the clipboard owner by a clipboard viewer window to request the name of a CF_OWNERDISPLAY clipboard format.
    ''' </summary>
    ''' <remarks></remarks>
    WM_ASKCBFORMATNAME = &H30C

    ''' <summary>
    '''The WM_CANCELJOURNAL message is posted to an application when a user cancels the application's journaling activities. The message is posted with a NULL window handle.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CANCELJOURNAL = &H4B

    ''' <summary>
    '''The WM_CANCELMODE message is sent to cancel certain modes such as mouse capture. For example the system sends this message to the active window when a dialog box or message box is displayed. Certain functions also send this message explicitly to the specified window regardless of whether it is the active window. For example the EnableWindow function sends this message when disabling the specified window.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CANCELMODE = &H1F

    ''' <summary>
    '''The WM_CAPTURECHANGED message is sent to the window that is losing the mouse capture.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CAPTURECHANGED = &H215

    ''' <summary>
    '''The WM_CHANGECBCHAIN message is sent to the first window in the clipboard viewer chain when a window is being removed from the chain.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CHANGECBCHAIN = &H30D

    ''' <summary>
    '''An application sends the WM_CHANGEUISTATE message to indicate that the user interface (UI) state should be changed.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CHANGEUISTATE = &H127

    ''' <summary>
    '''The WM_CHAR message is posted to the window with the keyboard focus when a WM_KEYDOWN message is translated by the TranslateMessage function. The WM_CHAR message contains the character code of the key that was pressed.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CHAR = &H102

    ''' <summary>
    '''Sent by a list box with the LBS_WANTKEYBOARDINPUT style to its owner in response to a WM_CHAR message.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CHARTOITEM = &H2F

    ''' <summary>
    '''The WM_CHILDACTIVATE message is sent to a child window when the user clicks the window's title bar or when the window is activated moved or sized.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CHILDACTIVATE = &H22

    ''' <summary>
    '''An application sends a WM_CLEAR message to an edit control or combo box to delete (clear) the current selection if any from the edit control.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CLEAR = &H303

    ''' <summary>
    '''The WM_CLOSE message is sent as a signal that a window or an application should terminate.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CLOSE = &H10

    ''' <summary>
    '''The WM_COMMAND message is sent when the user selects a command item from a menu when a control sends a notification message to its parent window or when an accelerator keystroke is translated.
    ''' </summary>
    ''' <remarks></remarks>
    WM_COMMAND = &H111

    ''' <summary>
    '''The WM_COMPACTING message is sent to all top-level windows when the system detects more than 12.5 percent of system time over a 30- to 60-second interval is being spent compacting memory. This indicates that system memory is low.
    ''' </summary>
    ''' <remarks></remarks>
    WM_COMPACTING = &H41

    ''' <summary>
    '''The system sends the WM_COMPAREITEM message to determine the relative position of a new item in the sorted list of an owner-drawn combo box or list box. Whenever the application adds a new item the system sends this message to the owner of a combo box or list box created with the CBS_SORT or LBS_SORT style.
    ''' </summary>
    ''' <remarks></remarks>
    WM_COMPAREITEM = &H39

    ''' <summary>
    '''The WM_CONTEXTMENU message notifies a window that the user clicked the right mouse button (right-clicked) in the window.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CONTEXTMENU = &H7B

    ''' <summary>
    '''An application sends the WM_COPY message to an edit control or combo box to copy the current selection to the clipboard in CF_TEXT format.
    ''' </summary>
    ''' <remarks></remarks>
    WM_COPY = &H301

    ''' <summary>
    '''An application sends the WM_COPYDATA message to pass data to another application.
    ''' </summary>
    ''' <remarks></remarks>
    WM_COPYDATA = &H4A

    ''' <summary>
    '''The WM_CREATE message is sent when an application requests that a window be created by calling the CreateWindowEx or CreateWindow function. (The message is sent before the function returns.) The window procedure of the new window receives this message after the window is created but before the window becomes visible.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CREATE = &H1

    ''' <summary>
    '''The WM_CTLCOLORBTN message is sent to the parent window of a button before drawing the button. The parent window can change the button's text and background colors. However only owner-drawn buttons respond to the parent window processing this message.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CTLCOLORBTN = &H135

    ''' <summary>
    '''The WM_CTLCOLORDLG message is sent to a dialog box before the system draws the dialog box. By responding to this message the dialog box can set its text and background colors using the specified display device context handle.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CTLCOLORDLG = &H136

    ''' <summary>
    '''An edit control that is not read-only or disabled sends the WM_CTLCOLOREDIT message to its parent window when the control is about to be drawn. By responding to this message the parent window can use the specified device context handle to set the text and background colors of the edit control.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CTLCOLOREDIT = &H133

    ''' <summary>
    '''Sent to the parent window of a list box before the system draws the list box. By responding to this message the parent window can set the text and background colors of the list box by using the specified display device context handle.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CTLCOLORLISTBOX = &H134

    ''' <summary>
    '''The WM_CTLCOLORMSGBOX message is sent to the owner window of a message box before Windows draws the message box. By responding to this message the owner window can set the text and background colors of the message box by using the given display device context handle.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CTLCOLORMSGBOX = &H132

    ''' <summary>
    '''The WM_CTLCOLORSCROLLBAR message is sent to the parent window of a scroll bar control when the control is about to be drawn. By responding to this message the parent window can use the display context handle to set the background color of the scroll bar control.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CTLCOLORSCROLLBAR = &H137

    ''' <summary>
    '''A static control or an edit control that is read-only or disabled sends the WM_CTLCOLORSTATIC message to its parent window when the control is about to be drawn. By responding to this message the parent window can use the specified device context handle to set the text and background colors of the static control.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CTLCOLORSTATIC = &H138

    ''' <summary>
    '''An application sends a WM_CUT message to an edit control or combo box to delete (cut) the current selection if any in the edit control and copy the deleted text to the clipboard in CF_TEXT format.
    ''' </summary>
    ''' <remarks></remarks>
    WM_CUT = &H300

    ''' <summary>
    '''The WM_DEADCHAR message is posted to the window with the keyboard focus when a WM_KEYUP message is translated by the TranslateMessage function. WM_DEADCHAR specifies a character code generated by a dead key. A dead key is a key that generates a character such as the umlaut (double-dot) that is combined with another character to form a composite character. For example the umlaut-O character (?) is generated by typing the dead key for the umlaut character and then typing the O key.
    ''' </summary>
    ''' <remarks></remarks>
    WM_DEADCHAR = &H103

    ''' <summary>
    '''Sent to the owner of a list box or combo box when the list box or combo box is destroyed or when items are removed by the LB_DELETESTRING LB_RESETCONTENT CB_DELETESTRING or CB_RESETCONTENT message. The system sends a WM_DELETEITEM message for each deleted item. The system sends the WM_DELETEITEM message for any deleted list box or combo box item with nonzero item data.
    ''' </summary>
    ''' <remarks></remarks>
    WM_DELETEITEM = &H2D

    ''' <summary>
    '''The WM_DESTROY message is sent when a window is being destroyed. It is sent to the window procedure of the window being destroyed after the window is removed from the screen. This message is sent first to the window being destroyed and then to the child windows (if any) as they are destroyed. During the processing of the message it can be assumed that all child windows still exist.
    ''' </summary>
    ''' <remarks></remarks>
    WM_DESTROY = &H2

    ''' <summary>
    '''The WM_DESTROYCLIPBOARD message is sent to the clipboard owner when a call to the EmptyClipboard function empties the clipboard.
    ''' </summary>
    ''' <remarks></remarks>
    WM_DESTROYCLIPBOARD = &H307

    ''' <summary>
    '''Notifies an application of a change to the hardware configuration of a device or the computer.
    ''' </summary>
    ''' <remarks></remarks>
    WM_DEVICECHANGE = &H219

    ''' <summary>
    '''The WM_DEVMODECHANGE message is sent to all top-level windows whenever the user changes device-mode settings.
    ''' </summary>
    ''' <remarks></remarks>
    WM_DEVMODECHANGE = &H1B

    ''' <summary>
    '''The WM_DISPLAYCHANGE message is sent to all windows when the display resolution has changed.
    ''' </summary>
    ''' <remarks></remarks>
    WM_DISPLAYCHANGE = &H7E

    ''' <summary>
    '''The WM_DRAWCLIPBOARD message is sent to the first window in the clipboard viewer chain when the content of the clipboard changes. This enables a clipboard viewer window to display the new content of the clipboard.
    ''' </summary>
    ''' <remarks></remarks>
    WM_DRAWCLIPBOARD = &H308

    ''' <summary>
    '''The WM_DRAWITEM message is sent to the parent window of an owner-drawn button combo box list box or menu when a visual aspect of the button combo box list box or menu has changed.
    ''' </summary>
    ''' <remarks></remarks>
    WM_DRAWITEM = &H2B

    ''' <summary>
    '''Sent when the user drops a file on the window of an application that has registered itself as a recipient of dropped files.
    ''' </summary>
    ''' <remarks></remarks>
    WM_DROPFILES = &H233

    ''' <summary>
    '''The WM_ENABLE message is sent when an application changes the enabled state of a window. It is sent to the window whose enabled state is changing. This message is sent before the EnableWindow function returns but after the enabled state (WS_DISABLED style bit) of the window has changed.
    ''' </summary>
    ''' <remarks></remarks>
    WM_ENABLE = &HA

    ''' <summary>
    '''The WM_ENDSESSION message is sent to an application after the system processes the results of the WM_QUERYENDSESSION message. The WM_ENDSESSION message informs the application whether the session is ending.
    ''' </summary>
    ''' <remarks></remarks>
    WM_ENDSESSION = &H16

    ''' <summary>
    '''The WM_ENTERIDLE message is sent to the owner window of a modal dialog box or menu that is entering an idle state. A modal dialog box or menu enters an idle state when no messages are waiting in its queue after it has processed one or more previous messages.
    ''' </summary>
    ''' <remarks></remarks>
    WM_ENTERIDLE = &H121

    ''' <summary>
    '''The WM_ENTERMENULOOP message informs an application's main window procedure that a menu modal loop has been entered.
    ''' </summary>
    ''' <remarks></remarks>
    WM_ENTERMENULOOP = &H211

    ''' <summary>
    '''The WM_ENTERSIZEMOVE message is sent one time to a window after it enters the moving or sizing modal loop. The window enters the moving or sizing modal loop when the user clicks the window's title bar or sizing border or when the window passes the WM_SYSCOMMAND message to the DefWindowProc function and the wParam parameter of the message specifies the SC_MOVE or SC_SIZE value. The operation is complete when DefWindowProc returns.
    ''' </summary>
    ''' <remarks></remarks>
    WM_ENTERSIZEMOVE = &H231

    ''' <summary>
    '''The WM_ERASEBKGND message is sent when the window background must be erased (for example when a window is resized). The message is sent to prepare an invalidated portion of a window for painting.
    ''' </summary>
    ''' <remarks></remarks>
    WM_ERASEBKGND = &H14

    ''' <summary>
    '''The WM_EXITMENULOOP message informs an application's main window procedure that a menu modal loop has been exited.
    ''' </summary>
    ''' <remarks></remarks>
    WM_EXITMENULOOP = &H212

    ''' <summary>
    '''The WM_EXITSIZEMOVE message is sent one time to a window after it has exited the moving or sizing modal loop. The window enters the moving or sizing modal loop when the user clicks the window's title bar or sizing border or when the window passes the WM_SYSCOMMAND message to the DefWindowProc function and the wParam parameter of the message specifies the SC_MOVE or SC_SIZE value. The operation is complete when DefWindowProc returns.
    ''' </summary>
    ''' <remarks></remarks>
    WM_EXITSIZEMOVE = &H232

    ''' <summary>
    '''An application sends the WM_FONTCHANGE message to all top-level windows in the system after changing the pool of font resources.
    ''' </summary>
    ''' <remarks></remarks>
    WM_FONTCHANGE = &H1D

    ''' <summary>
    '''The WM_GETDLGCODE message is sent to the window procedure associated with a control. By default the system handles all keyboard input to the control; the system interprets certain types of keyboard input as dialog box navigation keys. To override this default behavior the control can respond to the WM_GETDLGCODE message to indicate the types of input it wants to process itself.
    ''' </summary>
    ''' <remarks></remarks>
    WM_GETDLGCODE = &H87

    ''' <summary>
    '''An application sends a WM_GETFONT message to a control to retrieve the font with which the control is currently drawing its text.
    ''' </summary>
    ''' <remarks></remarks>
    WM_GETFONT = &H31

    ''' <summary>
    '''An application sends a WM_GETHOTKEY message to determine the hot key associated with a window.
    ''' </summary>
    ''' <remarks></remarks>
    WM_GETHOTKEY = &H33

    ''' <summary>
    '''The WM_GETICON message is sent to a window to retrieve a handle to the large or small icon associated with a window. The system displays the large icon in the ALT+TAB dialog and the small icon in the window caption.
    ''' </summary>
    ''' <remarks></remarks>
    WM_GETICON = &H7F

    ''' <summary>
    '''The WM_GETMINMAXINFO message is sent to a window when the size or position of the window is about to change. An application can use this message to override the window's default maximized size and position or its default minimum or maximum tracking size.
    ''' </summary>
    ''' <remarks></remarks>
    WM_GETMINMAXINFO = &H24

    ''' <summary>
    '''Active Accessibility sends the WM_GETOBJECT message to obtain information about an accessible object contained in a server application. Applications never send this message directly. It is sent only by Active Accessibility in response to calls to AccessibleObjectFromPoint AccessibleObjectFromEvent or AccessibleObjectFromWindow. However server applications handle this message.
    ''' </summary>
    ''' <remarks></remarks>
    WM_GETOBJECT = &H3D

    ''' <summary>
    '''An application sends a WM_GETTEXT message to copy the text that corresponds to a window into a buffer provided by the caller.
    ''' </summary>
    ''' <remarks></remarks>
    WM_GETTEXT = &HD

    ''' <summary>
    '''An application sends a WM_GETTEXTLENGTH message to determine the length in characters of the text associated with a window.
    ''' </summary>
    ''' <remarks></remarks>
    WM_GETTEXTLENGTH = &HE

    ''' <summary>
    '''Definition Needed
    ''' </summary>
    ''' <remarks></remarks>
    WM_HANDHELDFIRST = &H358

    ''' <summary>
    '''Definition Needed
    ''' </summary>
    ''' <remarks></remarks>
    WM_HANDHELDLAST = &H35F

    ''' <summary>
    '''Indicates that the user pressed the F1 key. If a menu is active when F1 is pressed WM_HELP is sent to the window associated with the menu; otherwise WM_HELP is sent to the window that has the keyboard focus. If no window has the keyboard focus WM_HELP is sent to the currently active window.
    ''' </summary>
    ''' <remarks></remarks>
    WM_HELP = &H53

    ''' <summary>
    '''The WM_HOTKEY message is posted when the user presses a hot key registered by the RegisterHotKey function. The message is placed at the top of the message queue associated with the thread that registered the hot key.
    ''' </summary>
    ''' <remarks></remarks>
    WM_HOTKEY = &H312

    ''' <summary>
    '''This message is sent to a window when a scroll event occurs in the window's standard horizontal scroll bar. This message is also sent to the owner of a horizontal scroll bar control when a scroll event occurs in the control.
    ''' </summary>
    ''' <remarks></remarks>
    WM_HSCROLL = &H114

    ''' <summary>
    '''The WM_HSCROLLCLIPBOARD message is sent to the clipboard owner by a clipboard viewer window. This occurs when the clipboard contains data in the CF_OWNERDISPLAY format and an event occurs in the clipboard viewer's horizontal scroll bar. The owner should scroll the clipboard image and update the scroll bar values.
    ''' </summary>
    ''' <remarks></remarks>
    WM_HSCROLLCLIPBOARD = &H30E

    ''' <summary>
    '''Windows NT 3.51 and earlier: The WM_ICONERASEBKGND message is sent to a minimized window when the background of the icon must be filled before painting the icon. A window receives this message only if a class icon is defined for the window; otherwise WM_ERASEBKGND is sent. This message is not sent by newer versions of Windows.
    ''' </summary>
    ''' <remarks></remarks>
    WM_ICONERASEBKGND = &H27

    ''' <summary>
    '''Sent to an application when the IME gets a character of the conversion result. A window receives this message through its WindowProc function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_IME_CHAR = &H286

    ''' <summary>
    '''Sent to an application when the IME changes composition status as a result of a keystroke. A window receives this message through its WindowProc function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_IME_COMPOSITION = &H10F

    ''' <summary>
    '''Sent to an application when the IME window finds no space to extend the area for the composition window. A window receives this message through its WindowProc function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_IME_COMPOSITIONFULL = &H284

    ''' <summary>
    '''Sent by an application to direct the IME window to carry out the requested command. The application uses this message to control the IME window that it has created. To send this message the application calls the SendMessage function with the following parameters.
    ''' </summary>
    ''' <remarks></remarks>
    WM_IME_CONTROL = &H283

    ''' <summary>
    '''Sent to an application when the IME ends composition. A window receives this message through its WindowProc function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_IME_ENDCOMPOSITION = &H10E

    ''' <summary>
    '''Sent to an application by the IME to notify the application of a key press and to keep message order. A window receives this message through its WindowProc function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_IME_KEYDOWN = &H290

    ''' <summary>
    '''Definition Needed
    ''' </summary>
    ''' <remarks></remarks>
    WM_IME_KEYLAST = &H10F

    ''' <summary>
    '''Sent to an application by the IME to notify the application of a key release and to keep message order. A window receives this message through its WindowProc function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_IME_KEYUP = &H291

    ''' <summary>
    '''Sent to an application to notify it of changes to the IME window. A window receives this message through its WindowProc function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_IME_NOTIFY = &H282

    ''' <summary>
    '''Sent to an application to provide commands and request information. A window receives this message through its WindowProc function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_IME_REQUEST = &H288

    ''' <summary>
    '''Sent to an application when the operating system is about to change the current IME. A window receives this message through its WindowProc function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_IME_SELECT = &H285

    ''' <summary>
    '''Sent to an application when a window is activated. A window receives this message through its WindowProc function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_IME_SETCONTEXT = &H281

    ''' <summary>
    '''Sent immediately before the IME generates the composition string as a result of a keystroke. A window receives this message through its WindowProc function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_IME_STARTCOMPOSITION = &H10D

    ''' <summary>
    '''The WM_INITDIALOG message is sent to the dialog box procedure immediately before a dialog box is displayed. Dialog box procedures typically use this message to initialize controls and carry out any other initialization tasks that affect the appearance of the dialog box.
    ''' </summary>
    ''' <remarks></remarks>
    WM_INITDIALOG = &H110

    ''' <summary>
    '''The WM_INITMENU message is sent when a menu is about to become active. It occurs when the user clicks an item on the menu bar or presses a menu key. This allows the application to modify the menu before it is displayed.
    ''' </summary>
    ''' <remarks></remarks>
    WM_INITMENU = &H116

    ''' <summary>
    '''The WM_INITMENUPOPUP message is sent when a drop-down menu or submenu is about to become active. This allows an application to modify the menu before it is displayed without changing the entire menu.
    ''' </summary>
    ''' <remarks></remarks>
    WM_INITMENUPOPUP = &H117

    ''' <summary>
    '''The WM_INPUTLANGCHANGE message is sent to the topmost affected window after an application's input language has been changed. You should make any application-specific settings and pass the message to the DefWindowProc function which passes the message to all first-level child windows. These child windows can pass the message to DefWindowProc to have it pass the message to their child windows and so on.
    ''' </summary>
    ''' <remarks></remarks>
    WM_INPUTLANGCHANGE = &H51

    ''' <summary>
    '''The WM_INPUTLANGCHANGEREQUEST message is posted to the window with the focus when the user chooses a new input language either with the hotkey (specified in the Keyboard control panel application) or from the indicator on the system taskbar. An application can accept the change by passing the message to the DefWindowProc function or reject the change (and prevent it from taking place) by returning immediately.
    ''' </summary>
    ''' <remarks></remarks>
    WM_INPUTLANGCHANGEREQUEST = &H50

    ''' <summary>
    '''The WM_KEYDOWN message is posted to the window with the keyboard focus when a nonsystem key is pressed. A nonsystem key is a key that is pressed when the ALT key is not pressed.
    ''' </summary>
    ''' <remarks></remarks>
    WM_KEYDOWN = &H100

    ''' <summary>
    '''This message filters for keyboard messages.
    ''' </summary>
    ''' <remarks></remarks>
    WM_KEYFIRST = &H100

    ''' <summary>
    '''This message filters for keyboard messages.
    ''' </summary>
    ''' <remarks></remarks>
    WM_KEYLAST = &H108

    ''' <summary>
    '''The WM_KEYUP message is posted to the window with the keyboard focus when a nonsystem key is released. A nonsystem key is a key that is pressed when the ALT key is not pressed or a keyboard key that is pressed when a window has the keyboard focus.
    ''' </summary>
    ''' <remarks></remarks>
    WM_KEYUP = &H101

    ''' <summary>
    '''The WM_KILLFOCUS message is sent to a window immediately before it loses the keyboard focus.
    ''' </summary>
    ''' <remarks></remarks>
    WM_KILLFOCUS = &H8

    ''' <summary>
    '''The WM_LBUTTONDBLCLK message is posted when the user double-clicks the left mouse button while the cursor is in the client area of a window. If the mouse is not captured the message is posted to the window beneath the cursor. Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' <remarks></remarks>
    WM_LBUTTONDBLCLK = &H203

    ''' <summary>
    '''The WM_LBUTTONDOWN message is posted when the user presses the left mouse button while the cursor is in the client area of a window. If the mouse is not captured the message is posted to the window beneath the cursor. Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' <remarks></remarks>
    WM_LBUTTONDOWN = &H201

    ''' <summary>
    '''The WM_LBUTTONUP message is posted when the user releases the left mouse button while the cursor is in the client area of a window. If the mouse is not captured the message is posted to the window beneath the cursor. Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' <remarks></remarks>
    WM_LBUTTONUP = &H202

    ''' <summary>
    '''The WM_MBUTTONDBLCLK message is posted when the user double-clicks the middle mouse button while the cursor is in the client area of a window. If the mouse is not captured the message is posted to the window beneath the cursor. Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MBUTTONDBLCLK = &H209

    ''' <summary>
    '''The WM_MBUTTONDOWN message is posted when the user presses the middle mouse button while the cursor is in the client area of a window. If the mouse is not captured the message is posted to the window beneath the cursor. Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MBUTTONDOWN = &H207

    ''' <summary>
    '''The WM_MBUTTONUP message is posted when the user releases the middle mouse button while the cursor is in the client area of a window. If the mouse is not captured the message is posted to the window beneath the cursor. Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MBUTTONUP = &H208

    ''' <summary>
    '''An application sends the WM_MDIACTIVATE message to a multiple-document interface (MDI) client window to instruct the client window to activate a different MDI child window.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MDIACTIVATE = &H222

    ''' <summary>
    '''An application sends the WM_MDICASCADE message to a multiple-document interface (MDI) client window to arrange all its child windows in a cascade format.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MDICASCADE = &H227

    ''' <summary>
    '''An application sends the WM_MDICREATE message to a multiple-document interface (MDI) client window to create an MDI child window.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MDICREATE = &H220

    ''' <summary>
    '''An application sends the WM_MDIDESTROY message to a multiple-document interface (MDI) client window to close an MDI child window.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MDIDESTROY = &H221

    ''' <summary>
    '''An application sends the WM_MDIGETACTIVE message to a multiple-document interface (MDI) client window to retrieve the handle to the active MDI child window.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MDIGETACTIVE = &H229

    ''' <summary>
    '''An application sends the WM_MDIICONARRANGE message to a multiple-document interface (MDI) client window to arrange all minimized MDI child windows. It does not affect child windows that are not minimized.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MDIICONARRANGE = &H228

    ''' <summary>
    '''An application sends the WM_MDIMAXIMIZE message to a multiple-document interface (MDI) client window to maximize an MDI child window. The system resizes the child window to make its client area fill the client window. The system places the child window's window menu icon in the rightmost position of the frame window's menu bar and places the child window's restore icon in the leftmost position. The system also appends the title bar text of the child window to that of the frame window.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MDIMAXIMIZE = &H225

    ''' <summary>
    '''An application sends the WM_MDINEXT message to a multiple-document interface (MDI) client window to activate the next or previous child window.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MDINEXT = &H224

    ''' <summary>
    '''An application sends the WM_MDIREFRESHMENU message to a multiple-document interface (MDI) client window to refresh the window menu of the MDI frame window.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MDIREFRESHMENU = &H234

    ''' <summary>
    '''An application sends the WM_MDIRESTORE message to a multiple-document interface (MDI) client window to restore an MDI child window from maximized or minimized size.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MDIRESTORE = &H223

    ''' <summary>
    '''An application sends the WM_MDISETMENU message to a multiple-document interface (MDI) client window to replace the entire menu of an MDI frame window to replace the window menu of the frame window or both.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MDISETMENU = &H230

    ''' <summary>
    '''An application sends the WM_MDITILE message to a multiple-document interface (MDI) client window to arrange all of its MDI child windows in a tile format.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MDITILE = &H226

    ''' <summary>
    '''The WM_MEASUREITEM message is sent to the owner window of a combo box list box list view control or menu item when the control or menu is created.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MEASUREITEM = &H2C

    ''' <summary>
    '''The WM_MENUCHAR message is sent when a menu is active and the user presses a key that does not correspond to any mnemonic or accelerator key. This message is sent to the window that owns the menu.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MENUCHAR = &H120

    ''' <summary>
    '''The WM_MENUCOMMAND message is sent when the user makes a selection from a menu.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MENUCOMMAND = &H126

    ''' <summary>
    '''The WM_MENUDRAG message is sent to the owner of a drag-and-drop menu when the user drags a menu item.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MENUDRAG = &H123

    ''' <summary>
    '''The WM_MENUGETOBJECT message is sent to the owner of a drag-and-drop menu when the mouse cursor enters a menu item or moves from the center of the item to the top or bottom of the item.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MENUGETOBJECT = &H124

    ''' <summary>
    '''The WM_MENURBUTTONUP message is sent when the user releases the right mouse button while the cursor is on a menu item.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MENURBUTTONUP = &H122

    ''' <summary>
    '''The WM_MENUSELECT message is sent to a menu's owner window when the user selects a menu item.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MENUSELECT = &H11F

    ''' <summary>
    '''The WM_MOUSEACTIVATE message is sent when the cursor is in an inactive window and the user presses a mouse button. The parent window receives this message only if the child window passes it to the DefWindowProc function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MOUSEACTIVATE = &H21

    ''' <summary>
    '''Use WM_MOUSEFIRST to specify the first mouse message. Use the PeekMessage() Function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MOUSEFIRST = &H200

    ''' <summary>
    '''The WM_MOUSEHOVER message is posted to a window when the cursor hovers over the client area of the window for the period of time specified in a prior call to TrackMouseEvent.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MOUSEHOVER = &H2A1

    ''' <summary>
    '''Definition Needed
    ''' </summary>
    ''' <remarks></remarks>
    WM_MOUSELAST = &H20D

    ''' <summary>
    '''The WM_MOUSELEAVE message is posted to a window when the cursor leaves the client area of the window specified in a prior call to TrackMouseEvent.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MOUSELEAVE = &H2A3

    ''' <summary>
    '''The WM_MOUSEMOVE message is posted to a window when the cursor moves. If the mouse is not captured the message is posted to the window that contains the cursor. Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MOUSEMOVE = &H200

    ''' <summary>
    '''The WM_MOUSEWHEEL message is sent to the focus window when the mouse wheel is rotated. The DefWindowProc function propagates the message to the window's parent. There should be no internal forwarding of the message since DefWindowProc propagates it up the parent chain until it finds a window that processes it.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MOUSEWHEEL = &H20A

    ''' <summary>
    '''The WM_MOUSEHWHEEL message is sent to the focus window when the mouse's horizontal scroll wheel is tilted or rotated. The DefWindowProc function propagates the message to the window's parent. There should be no internal forwarding of the message since DefWindowProc propagates it up the parent chain until it finds a window that processes it.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MOUSEHWHEEL = &H20E

    ''' <summary>
    '''The WM_MOVE message is sent after a window has been moved.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MOVE = &H3

    ''' <summary>
    '''The WM_MOVING message is sent to a window that the user is moving. By processing this message an application can monitor the position of the drag rectangle and if needed change its position.
    ''' </summary>
    ''' <remarks></remarks>
    WM_MOVING = &H216

    ''' <summary>
    '''Non Client Area Activated Caption(Title) of the Form
    ''' </summary>
    ''' <remarks></remarks>
    WM_NCACTIVATE = &H86

    ''' <summary>
    '''The WM_NCCALCSIZE message is sent when the size and position of a window's client area must be calculated. By processing this message an application can control the content of the window's client area when the size or position of the window changes.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NCCALCSIZE = &H83

    ''' <summary>
    '''The WM_NCCREATE message is sent prior to the WM_CREATE message when a window is first created.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NCCREATE = &H81

    ''' <summary>
    '''The WM_NCDESTROY message informs a window that its nonclient area is being destroyed. The DestroyWindow function sends the WM_NCDESTROY message to the window following the WM_DESTROY message. WM_DESTROY is used to free the allocated memory object associated with the window.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NCDESTROY = &H82

    ''' <summary>
    '''The WM_NCHITTEST message is sent to a window when the cursor moves or when a mouse button is pressed or released. If the mouse is not captured the message is sent to the window beneath the cursor. Otherwise the message is sent to the window that has captured the mouse.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NCHITTEST = &H84

    ''' <summary>
    '''The WM_NCLBUTTONDBLCLK message is posted when the user double-clicks the left mouse button while the cursor is within the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse this message is not posted.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NCLBUTTONDBLCLK = &HA3

    ''' <summary>
    '''The WM_NCLBUTTONDOWN message is posted when the user presses the left mouse button while the cursor is within the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse this message is not posted.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NCLBUTTONDOWN = &HA1

    ''' <summary>
    '''The WM_NCLBUTTONUP message is posted when the user releases the left mouse button while the cursor is within the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse this message is not posted.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NCLBUTTONUP = &HA2

    ''' <summary>
    '''The WM_NCMBUTTONDBLCLK message is posted when the user double-clicks the middle mouse button while the cursor is within the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse this message is not posted.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NCMBUTTONDBLCLK = &HA9

    ''' <summary>
    '''The WM_NCMBUTTONDOWN message is posted when the user presses the middle mouse button while the cursor is within the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse this message is not posted.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NCMBUTTONDOWN = &HA7

    ''' <summary>
    '''The WM_NCMBUTTONUP message is posted when the user releases the middle mouse button while the cursor is within the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse this message is not posted.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NCMBUTTONUP = &HA8

    ''' <summary>
    ''' The WM_NCMOUSELEAVE message is posted to a window when the cursor leaves the nonclient area of the window specified in a prior call to TrackMouseEvent.
    ''' </summary>
    WM_NCMOUSELEAVE = &H2A2

    ''' <summary>
    '''The WM_NCMOUSEMOVE message is posted to a window when the cursor is moved within the nonclient area of the window. This message is posted to the window that contains the cursor. If a window has captured the mouse this message is not posted.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NCMOUSEMOVE = &HA0

    ''' <summary>
    '''The WM_NCPAINT message is sent to a window when its frame must be painted.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NCPAINT = &H85

    ''' <summary>
    '''The WM_NCRBUTTONDBLCLK message is posted when the user double-clicks the right mouse button while the cursor is within the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse this message is not posted.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NCRBUTTONDBLCLK = &HA6

    ''' <summary>
    '''The WM_NCRBUTTONDOWN message is posted when the user presses the right mouse button while the cursor is within the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse this message is not posted.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NCRBUTTONDOWN = &HA4

    ''' <summary>
    '''The WM_NCRBUTTONUP message is posted when the user releases the right mouse button while the cursor is within the nonclient area of a window. This message is posted to the window that contains the cursor. If a window has captured the mouse this message is not posted.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NCRBUTTONUP = &HA5

    ''' <summary>
    '''The WM_NEXTDLGCTL message is sent to a dialog box procedure to set the keyboard focus to a different control in the dialog box
    ''' </summary>
    ''' <remarks></remarks>
    WM_NEXTDLGCTL = &H28

    ''' <summary>
    '''The WM_NEXTMENU message is sent to an application when the right or left arrow key is used to switch between the menu bar and the system menu.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NEXTMENU = &H213

    ''' <summary>
    '''Sent by a common control to its parent window when an event has occurred or the control requires some information.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NOTIFY = &H4E

    ''' <summary>
    '''Determines if a window accepts ANSI or Unicode structures in the WM_NOTIFY notification message. WM_NOTIFYFORMAT messages are sent from a common control to its parent window and from the parent window to the common control.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NOTIFYFORMAT = &H55

    ''' <summary>
    '''The WM_NULL message performs no operation. An application sends the WM_NULL message if it wants to post a message that the recipient window will ignore.
    ''' </summary>
    ''' <remarks></remarks>
    WM_NULL = &H0

    ''' <summary>
    '''Occurs when the control needs repainting
    ''' </summary>
    ''' <remarks></remarks>
    WM_PAINT = &HF

    ''' <summary>
    '''The WM_PAINTCLIPBOARD message is sent to the clipboard owner by a clipboard viewer window when the clipboard contains data in the CF_OWNERDISPLAY format and the clipboard viewer's client area needs repainting.
    ''' </summary>
    ''' <remarks></remarks>
    WM_PAINTCLIPBOARD = &H309

    ''' <summary>
    '''Windows NT 3.51 and earlier: The WM_PAINTICON message is sent to a minimized window when the icon is to be painted. This message is not sent by newer versions of Microsoft Windows except in unusual circumstances explained in the Remarks.
    ''' </summary>
    ''' <remarks></remarks>
    WM_PAINTICON = &H26

    ''' <summary>
    '''This message is sent by the OS to all top-level and overlapped windows after the window with the keyboard focus realizes its logical palette. This message enables windows that do not have the keyboard focus to realize their logical palettes and update their client areas.
    ''' </summary>
    ''' <remarks></remarks>
    WM_PALETTECHANGED = &H311

    ''' <summary>
    '''The WM_PALETTEISCHANGING message informs applications that an application is going to realize its logical palette.
    ''' </summary>
    ''' <remarks></remarks>
    WM_PALETTEISCHANGING = &H310

    ''' <summary>
    '''The WM_PARENTNOTIFY message is sent to the parent of a child window when the child window is created or destroyed or when the user clicks a mouse button while the cursor is over the child window. When the child window is being created the system sends WM_PARENTNOTIFY just before the CreateWindow or CreateWindowEx function that creates the window returns. When the child window is being destroyed the system sends the message before any processing to destroy the window takes place.
    ''' </summary>
    ''' <remarks></remarks>
    WM_PARENTNOTIFY = &H210

    ''' <summary>
    '''An application sends a WM_PASTE message to an edit control or combo box to copy the current content of the clipboard to the edit control at the current caret position. Data is inserted only if the clipboard contains data in CF_TEXT format.
    ''' </summary>
    ''' <remarks></remarks>
    WM_PASTE = &H302

    ''' <summary>
    '''Definition Needed
    ''' </summary>
    ''' <remarks></remarks>
    WM_PENWINFIRST = &H380

    ''' <summary>
    '''Definition Needed
    ''' </summary>
    ''' <remarks></remarks>
    WM_PENWINLAST = &H38F

    ''' <summary>
    '''Notifies applications that the system typically a battery-powered personal computer is about to enter a suspended mode. Obsolete : use POWERBROADCAST instead
    ''' </summary>
    ''' <remarks></remarks>
    WM_POWER = &H48

    ''' <summary>
    '''Notifies applications that a power-management event has occurred.
    ''' </summary>
    ''' <remarks></remarks>
    WM_POWERBROADCAST = &H218

    ''' <summary>
    '''The WM_PRINT message is sent to a window to request that it draw itself in the specified device context most commonly in a printer device context.
    ''' </summary>
    ''' <remarks></remarks>
    WM_PRINT = &H317

    ''' <summary>
    '''The WM_PRINTCLIENT message is sent to a window to request that it draw its client area in the specified device context most commonly in a printer device context.
    ''' </summary>
    ''' <remarks></remarks>
    WM_PRINTCLIENT = &H318

    ''' <summary>
    '''The WM_QUERYDRAGICON message is sent to a minimized (iconic) window. The window is about to be dragged by the user but does not have an icon defined for its class. An application can return a handle to an icon or cursor. The system displays this cursor or icon while the user drags the icon.
    ''' </summary>
    ''' <remarks></remarks>
    WM_QUERYDRAGICON = &H37

    ''' <summary>
    '''The WM_QUERYENDSESSION message is sent when the user chooses to end the session or when an application calls one of the system shutdown functions. If any application returns zero the session is not ended. The system stops sending WM_QUERYENDSESSION messages as soon as one application returns zero. After processing this message the system sends the WM_ENDSESSION message with the wParam parameter set to the results of the WM_QUERYENDSESSION message.
    ''' </summary>
    ''' <remarks></remarks>
    WM_QUERYENDSESSION = &H11

    ''' <summary>
    '''This message informs a window that it is about to receive the keyboard focus giving the window the opportunity to realize its logical palette when it receives the focus.
    ''' </summary>
    ''' <remarks></remarks>
    WM_QUERYNEWPALETTE = &H30F

    ''' <summary>
    '''The WM_QUERYOPEN message is sent to an icon when the user requests that the window be restored to its previous size and position.
    ''' </summary>
    ''' <remarks></remarks>
    WM_QUERYOPEN = &H13

    ''' <summary>
    '''The WM_QUEUESYNC message is sent by a computer-based training (CBT) application to separate user-input messages from other messages sent through the WH_JOURNALPLAYBACK Hook procedure.
    ''' </summary>
    ''' <remarks></remarks>
    WM_QUEUESYNC = &H23

    ''' <summary>
    '''Once received it ends the application's Message Loop signaling the application to end. It can be sent by pressing Alt+F4 Clicking the X in the upper right-hand of the program or going to File->Exit.
    ''' </summary>
    ''' <remarks></remarks>
    WM_QUIT = &H12

    ''' <summary>
    '''he WM_RBUTTONDBLCLK message is posted when the user double-clicks the right mouse button while the cursor is in the client area of a window. If the mouse is not captured the message is posted to the window beneath the cursor. Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' <remarks></remarks>
    WM_RBUTTONDBLCLK = &H206

    ''' <summary>
    '''The WM_RBUTTONDOWN message is posted when the user presses the right mouse button while the cursor is in the client area of a window. If the mouse is not captured the message is posted to the window beneath the cursor. Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' <remarks></remarks>
    WM_RBUTTONDOWN = &H204

    ''' <summary>
    '''The WM_RBUTTONUP message is posted when the user releases the right mouse button while the cursor is in the client area of a window. If the mouse is not captured the message is posted to the window beneath the cursor. Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' <remarks></remarks>
    WM_RBUTTONUP = &H205

    ''' <summary>
    '''The WM_RENDERALLFORMATS message is sent to the clipboard owner before it is destroyed if the clipboard owner has delayed rendering one or more clipboard formats. For the content of the clipboard to remain available to other applications the clipboard owner must render data in all the formats it is capable of generating and place the data on the clipboard by calling the SetClipboardData function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_RENDERALLFORMATS = &H306

    ''' <summary>
    '''The WM_RENDERFORMAT message is sent to the clipboard owner if it has delayed rendering a specific clipboard format and if an application has requested data in that format. The clipboard owner must render data in the specified format and place it on the clipboard by calling the SetClipboardData function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_RENDERFORMAT = &H305

    ''' <summary>
    '''The WM_SETCURSOR message is sent to a window if the mouse causes the cursor to move within a window and mouse input is not captured.
    ''' </summary>
    ''' <remarks></remarks>
    WM_SETCURSOR = &H20

    ''' <summary>
    '''When the controll got the focus
    ''' </summary>
    ''' <remarks></remarks>
    WM_SETFOCUS = &H7

    ''' <summary>
    '''An application sends a WM_SETFONT message to specify the font that a control is to use when drawing text.
    ''' </summary>
    ''' <remarks></remarks>
    WM_SETFONT = &H30

    ''' <summary>
    '''An application sends a WM_SETHOTKEY message to a window to associate a hot key with the window. When the user presses the hot key the system activates the window.
    ''' </summary>
    ''' <remarks></remarks>
    WM_SETHOTKEY = &H32

    ''' <summary>
    '''An application sends the WM_SETICON message to associate a new large or small icon with a window. The system displays the large icon in the ALT+TAB dialog box and the small icon in the window caption.
    ''' </summary>
    ''' <remarks></remarks>
    WM_SETICON = &H80

    ''' <summary>
    '''An application sends the WM_SETREDRAW message to a window to allow changes in that window to be redrawn or to prevent changes in that window from being redrawn.
    ''' </summary>
    ''' <remarks></remarks>
    WM_SETREDRAW = &HB

    ''' <summary>
    '''Text / Caption changed on the control. An application sends a WM_SETTEXT message to set the text of a window.
    ''' </summary>
    ''' <remarks></remarks>
    WM_SETTEXT = &HC

    ''' <summary>
    '''An application sends the WM_SETTINGCHANGE message to all top-level windows after making a change to the WIN.INI file. The SystemParametersInfo function sends this message after an application uses the function to change a setting in WIN.INI.
    ''' </summary>
    ''' <remarks></remarks>
    WM_SETTINGCHANGE = &H1A

    ''' <summary>
    '''The WM_SHOWWINDOW message is sent to a window when the window is about to be hidden or shown
    ''' </summary>
    ''' <remarks></remarks>
    WM_SHOWWINDOW = &H18

    ''' <summary>
    '''The WM_SIZE message is sent to a window after its size has changed.
    ''' </summary>
    ''' <remarks></remarks>
    WM_SIZE = &H5

    ''' <summary>
    '''The WM_SIZECLIPBOARD message is sent to the clipboard owner by a clipboard viewer window when the clipboard contains data in the CF_OWNERDISPLAY format and the clipboard viewer's client area has changed size.
    ''' </summary>
    ''' <remarks></remarks>
    WM_SIZECLIPBOARD = &H30B

    ''' <summary>
    '''The WM_SIZING message is sent to a window that the user is resizing. By processing this message an application can monitor the size and position of the drag rectangle and if needed change its size or position.
    ''' </summary>
    ''' <remarks></remarks>
    WM_SIZING = &H214

    ''' <summary>
    '''The WM_SPOOLERSTATUS message is sent from Print Manager whenever a job is added to or removed from the Print Manager queue.
    ''' </summary>
    ''' <remarks></remarks>
    WM_SPOOLERSTATUS = &H2A

    ''' <summary>
    '''The WM_STYLECHANGED message is sent to a window after the SetWindowLong function has changed one or more of the window's styles.
    ''' </summary>
    ''' <remarks></remarks>
    WM_STYLECHANGED = &H7D

    ''' <summary>
    '''The WM_STYLECHANGING message is sent to a window when the SetWindowLong function is about to change one or more of the window's styles.
    ''' </summary>
    ''' <remarks></remarks>
    WM_STYLECHANGING = &H7C

    ''' <summary>
    '''The WM_SYNCPAINT message is used to synchronize painting while avoiding linking independent GUI threads.
    ''' </summary>
    ''' <remarks></remarks>
    WM_SYNCPAINT = &H88

    ''' <summary>
    '''The WM_SYSCHAR message is posted to the window with the keyboard focus when a WM_SYSKEYDOWN message is translated by the TranslateMessage function. It specifies the character code of a system character key — that is a character key that is pressed while the ALT key is down.
    ''' </summary>
    ''' <remarks></remarks>
    WM_SYSCHAR = &H106

    ''' <summary>
    '''This message is sent to all top-level windows when a change is made to a system color setting.
    ''' </summary>
    ''' <remarks></remarks>
    WM_SYSCOLORCHANGE = &H15

    ''' <summary>
    '''A window receives this message when the user chooses a command from the Window menu (formerly known as the system or control menu) or when the user chooses the maximize button minimize button restore button or close button.
    ''' </summary>
    ''' <remarks></remarks>
    WM_SYSCOMMAND = &H112

    ''' <summary>
    '''The WM_SYSDEADCHAR message is sent to the window with the keyboard focus when a WM_SYSKEYDOWN message is translated by the TranslateMessage function. WM_SYSDEADCHAR specifies the character code of a system dead key — that is a dead key that is pressed while holding down the ALT key.
    ''' </summary>
    ''' <remarks></remarks>
    WM_SYSDEADCHAR = &H107

    ''' <summary>
    '''The WM_SYSKEYDOWN message is posted to the window with the keyboard focus when the user presses the F10 key (which activates the menu bar) or holds down the ALT key and then presses another key. It also occurs when no window currently has the keyboard focus; in this case the WM_SYSKEYDOWN message is sent to the active window. The window that receives the message can distinguish between these two contexts by checking the context code in the lParam parameter.
    ''' </summary>
    ''' <remarks></remarks>
    WM_SYSKEYDOWN = &H104

    ''' <summary>
    '''The WM_SYSKEYUP message is posted to the window with the keyboard focus when the user releases a key that was pressed while the ALT key was held down. It also occurs when no window currently has the keyboard focus; in this case the WM_SYSKEYUP message is sent to the active window. The window that receives the message can distinguish between these two contexts by checking the context code in the lParam parameter.
    ''' </summary>
    ''' <remarks></remarks>
    WM_SYSKEYUP = &H105

    ''' <summary>
    '''Sent to an application that has initiated a training card with Microsoft Windows Help. The message informs the application when the user clicks an authorable button. An application initiates a training card by specifying the HELP_TCARD command in a call to the WinHelp function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_TCARD = &H52

    ''' <summary>
    '''A message that is sent whenever there is a change in the system time.
    ''' </summary>
    ''' <remarks></remarks>
    WM_TIMECHANGE = &H1E

    ''' <summary>
    '''The WM_TIMER message is posted to the installing thread's message queue when a timer expires. The message is posted by the GetMessage or PeekMessage function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_TIMER = &H113

    ''' <summary>
    '''An application sends a WM_UNDO message to an edit control to undo the last operation. When this message is sent to an edit control the previously deleted text is restored or the previously added text is deleted.
    ''' </summary>
    ''' <remarks></remarks>
    WM_UNDO = &H304

    ''' <summary>
    '''The WM_UNINITMENUPOPUP message is sent when a drop-down menu or submenu has been destroyed.
    ''' </summary>
    ''' <remarks></remarks>
    WM_UNINITMENUPOPUP = &H125

    ''' <summary>
    '''The WM_USER constant is used by applications to help define private messages for use by private window classes usually of the form WM_USER+X where X is an integer value.
    ''' </summary>
    ''' <remarks></remarks>
    WM_USER = &H400

    ''' <summary>
    '''The WM_USERCHANGED message is sent to all windows after the user has logged on or off. When the user logs on or off the system updates the user-specific settings. The system sends this message immediately after updating the settings.
    ''' </summary>
    ''' <remarks></remarks>
    WM_USERCHANGED = &H54

    ''' <summary>
    '''Sent by a list box with the LBS_WANTKEYBOARDINPUT style to its owner in response to a WM_KEYDOWN message.
    ''' </summary>
    ''' <remarks></remarks>
    WM_VKEYTOITEM = &H2E

    ''' <summary>
    '''The WM_VSCROLL message is sent to a window when a scroll event occurs in the window's standard vertical scroll bar. This message is also sent to the owner of a vertical scroll bar control when a scroll event occurs in the control.
    ''' </summary>
    ''' <remarks></remarks>
    WM_VSCROLL = &H115

    ''' <summary>
    '''The WM_VSCROLLCLIPBOARD message is sent to the clipboard owner by a clipboard viewer window when the clipboard contains data in the CF_OWNERDISPLAY format and an event occurs in the clipboard viewer's vertical scroll bar. The owner should scroll the clipboard image and update the scroll bar values.
    ''' </summary>
    ''' <remarks></remarks>
    WM_VSCROLLCLIPBOARD = &H30A

    ''' <summary>
    '''The WM_WINDOWPOSCHANGED message is sent to a window whose size position or place in the Z order has changed as a result of a call to the SetWindowPos function or another window-management function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_WINDOWPOSCHANGED = &H47

    ''' <summary>
    '''The WM_WINDOWPOSCHANGING message is sent to a window whose size position or place in the Z order is about to change as a result of a call to the SetWindowPos function or another window-management function.
    ''' </summary>
    ''' <remarks></remarks>
    WM_WINDOWPOSCHANGING = &H46

    ''' <summary>
    '''An application sends the WM_WININICHANGE message to all top-level windows after making a change to the WIN.INI file. The SystemParametersInfo function sends this message after an application uses the function to change a setting in WIN.INI. Note The WM_WININICHANGE message is provided only for compatibility with earlier versions of the system. Applications should use the WM_SETTINGCHANGE message.
    ''' </summary>
    ''' <remarks></remarks>
    WM_WININICHANGE = &H1A

    ''' <summary>
    '''Definition Needed
    ''' </summary>
    ''' <remarks></remarks>
    WM_XBUTTONDBLCLK = &H20D

    ''' <summary>
    '''Definition Needed
    ''' </summary>
    ''' <remarks></remarks>
    WM_XBUTTONDOWN = &H20B

    ''' <summary>
    '''Definition Needed
    ''' </summary>
    ''' <remarks></remarks>
    WM_XBUTTONUP = &H20C
End Enum
```

## VB Definition with better documentation ( by ElektroStudios ), using .Net naming convennions and urls to MSDN:
```cs
''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The system sends or posts a system-defined message when it communicates with an application. 
    ''' <para></para>
    ''' It uses these messages to control the operations of applications and to provide input and other information for applications to process. 
    ''' <para></para>
    ''' An application can also send or post system-defined messages.
    ''' <para></para>
    ''' Applications generally use these messages to control the operation of control windows created by using preregistered window classes.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms644927%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    Public Enum WindowsMessages As Integer

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The <see cref="Null"/> message performs no operation.
    ''' <para></para>
    ''' An application sends the <see cref="Null"/> message if it wants to 
    ''' post a message that the recipient window will ignore.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    Null = &H0

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Notifies an application that an MCI device has completed an operation. 
    ''' MCI devices send this message only when the <c>MCI_NOTIFY</c> flag is used.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' Reason for the notification.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' Identifier of the device initiating the callback function.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/dd757358%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    MmMciNotify = 953

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Notifies a window that the user generated an application command event, for example, 
    ''' by clicking an application command button using the mouse or typing an application command key on the keyboard.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' A handle to the window where the user clicked the button or pressed the key.
    ''' This can be a child window of the window receiving the message.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/>
    ''' See Remarks.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/es-es/library/windows/desktop/ms646275%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WMAppcommand = &H319

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to all top-level windows in the system, including disabled or invisible unowned windows.
    ''' <para></para>
    ''' The function does not return until each window has timed out.
    ''' Therefore, the total wait time can be up to the value of uTimeout multiplied by the number of top-level windows.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms644952%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    HwndBroadcast = &HFFFF

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' A window receives this message when the user chooses a command from the Window menu 
    ''' (formerly known as the system or control menu) or when the user chooses the maximize button, 
    ''' minimize button, restore button, or close button.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/>
    ''' The type of system command requested
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/>
    ''' The low-order word specifies the horizontal position of the cursor, in screen coordinates, 
    ''' if a window menu command is chosen with the mouse. 
    ''' <para></para>
    ''' Otherwise, this parameter is not used.
    ''' <para></para>
    ''' The high-order word specifies the vertical position of the cursor, in screen coordinates, 
    ''' if a window menu command is chosen with the mouse. 
    ''' <para></para>
    ''' This parameter is –1 if the command is chosen using a system accelerator, or zero if using a mnemonic.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' In <see cref="WmSysCommand"/> messages, 
    ''' the four low-order bits of the wParam parameter are used internally by the system.
    ''' <para></para>
    ''' To obtain the correct result when testing the value of wParam, 
    ''' an application must combine the value <c>0xHFFF0</c> (<c>&HFFF0</c> in Vb.Net) with the wParam value by 
    ''' using the bitwise <see langword="And"/> operator.
    ''' <para></para>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms646360%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmSysCommand = &H112

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' A message that is sent to all top-level windows when 
    ''' the SystemParametersInfo function changes a system-wide setting or when policy settings have changed.
    ''' <para></para>
    ''' Applications should send <see cref="WindowsMessages.WmSettingchange"/> to all top-level windows when 
    ''' they make changes to system parameters
    ''' <para></para>
    ''' This message cannot be sent directly to a single window.
    ''' <para></para>
    ''' To send the <see cref="WindowsMessages.WmSettingchange"/> message to all top-level windows, 
    ''' use the <see cref="NativeMethods.SendMessageTimeout"/> function with the <paramref name="hwnd"/> parameter set to 
    ''' <see cref="WindowsMessages.HwndBroadcast"/>.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' See Remakrs.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' See Remakrs.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms725497%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmSettingchange = &H1A

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Message sent when the user selects a command item from a menu,
    ''' when a control sends a notification message to its parent window,
    ''' or when an accelerator keystroke is translated.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' For a description of this parameter, see Remarks.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' For a description of this parameter, see Remarks.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms647591%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmCommand = &H111

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Copies the text that corresponds to a window into a buffer provided by the caller.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' The maximum number of characters to be copied, including the terminating null character.
    ''' <para></para>
    ''' ANSI applications may have the string in the buffer reduced in size 
    ''' (to a minimum of half that of the wParam value) due to conversion from ANSI to Unicode.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' A pointer to the buffer that is to receive the text.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms632627%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmGetText = &HD

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Determines the length, in characters, of the text associated with a window.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' This parameter is not used and must be zero
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' This parameter is not used and must be zero
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms632628%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmGetTextLength = &HE

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Sets the text of a window.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' This parameter is not used
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' A pointer to a null-terminated string that is the window text.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms632644%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmSetText = &HC

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Sent as a signal that a window or an application should terminate.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' This parameter is not used.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' This parameter is not used.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms632617%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmClose = &H10

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Sent after a window has been moved.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' This parameter is not used.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' The x and y coordinates of the upper-left corner of the client area of the window. 
    ''' <para></para>
    ''' The low-order word contains the x-coordinate while the high-order word contains the y coordinate. 
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms632631%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmMove = &H3

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Posted when the user presses the left mouse button while the cursor is within the nonclient area of a window.
    ''' <para></para>
    ''' This message is posted to the window that contains the cursor. 
    ''' <para></para>
    ''' If a window has captured the mouse, this message is not posted.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' The hit-test value returned by the <c>DefWindowProc</c> function as a 
    ''' result of processing the <see cref="WindowsMessages.WmNchitTest"/> message.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' A <c>POINTS</c> structure that contains the x- and y-coordinates of the cursor. 
    ''' <para></para>
    ''' The coordinates are relative to the upper-left corner of the screen. 
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms645620%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNcLButtonDown = &HA1

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Posted when the user releases the left mouse button while the cursor is within the nonclient area of a window.
    ''' <para></para>
    ''' This message is posted to the window that contains the cursor. 
    ''' <para></para>
    ''' If a window has captured the mouse, this message is not posted.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' The hit-test value returned by the <c>DefWindowProc</c> function as a 
    ''' result of processing the <see cref="WindowsMessages.WmNchitTest"/> message.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' A <c>POINTS</c> structure that contains the x- and y-coordinates of the cursor. 
    ''' <para></para>
    ''' The coordinates are relative to the upper-left corner of the screen. 
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms645621%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNcLButtonUp = &HA2

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Posted when the user presses the right mouse button while the cursor is within the nonclient area of a window. 
    ''' <para></para>
    ''' This message is posted to the window that contains the cursor. 
    ''' <para></para>
    ''' If a window has captured the mouse, this message is not posted.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' The hit-test value returned by the <c>DefWindowProc</c> function as a 
    ''' result of processing the <see cref="WindowsMessages.WmNchitTest"/> message.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' A <c>POINTS</c> structure that contains the x- and y-coordinates of the cursor.
    ''' <para></para>
    ''' The coordinates are relative to the upper-left corner of the screen. 
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms645629%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNcRButtonDown = &HA4

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Posted when the user releases the right mouse button while the cursor is within the nonclient area of a window.
    ''' <para></para>
    ''' This message is posted to the window that contains the cursor. 
    ''' <para></para>
    ''' If a window has captured the mouse, this message is not posted.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' The hit-test value returned by the <c>DefWindowProc</c> function as a 
    ''' result of processing the <see cref="WindowsMessages.WmNchitTest"/> message.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' A <c>POINTS</c> structure that contains the x- and y-coordinates of the cursor.
    ''' <para></para>
    ''' The coordinates are relative to the upper-left corner of the screen. 
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms645630%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNcRButtonUp = &HA5

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Sent when a menu is about to become active. 
    ''' <para></para>
    ''' It occurs when the user clicks an item on the menu bar or presses a menu key. 
    ''' <para></para>
    ''' This allows the application to modify the menu before it is displayed. 
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' A handle to the menu to be initialized.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' This parameter is not used.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms646344%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmInitMenu = &H116

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Sent when a drop-down menu or submenu is about to become active.
    ''' <para></para>
    ''' This allows an application to modify the menu before it is displayed, 
    ''' without changing the entire menu. 
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' A handle to the drop-down menu or submenu. 
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' The low-order word specifies the zero-based relative position of the
    ''' menu item that opens the drop-down menu or submenu.
    ''' <para></para>
    ''' The high-order word indicates whether the drop-down menu is the window menu. 
    ''' <para></para>
    ''' If the menu is the window menu, this parameter is <see langword="True"/>; otherwise, it is <see langword="False"/>.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms646347%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmInitMenuPopup = &H117

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Sent to a window in order to determine what part of the window corresponds to a particular screen coordinate.
    ''' <para></para>
    ''' This can happen, for example, when the cursor moves, when a mouse button is pressed or released, 
    ''' or in response to a call to a function such as <c>WindowFromPoint</c>.
    ''' <para></para>
    ''' If the mouse is not captured, the message is sent to the window beneath the cursor. 
    ''' Otherwise, the message is sent to the window that has captured the mouse.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' This parameter is not used.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' The low-order word specifies the x-coordinate of the cursor. 
    ''' The coordinate is relative to the upper-left corner of the screen.
    ''' <para></para>
    ''' The high-order word specifies the y-coordinate of the cursor. 
    ''' The coordinate is relative to the upper-left corner of the screen.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/es-es/library/windows/desktop/ms645618%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNchitTest = &H84

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Posted when the user presses a hot key registered by the <c>RegisterHotKey</c> function. 
    ''' <para></para>
    ''' The message is placed at the top of the message queue associated with the thread that registered the hot key.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' The identifier of the hot key that generated the message.
    ''' If the message was generated by a system-defined hot key.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' The low-order word specifies the keys that were to be pressed in 
    ''' combination with the key specified by the high-order word to generate the 
    ''' <see cref="WindowsMessages.WmHotkey"/> message.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms646279%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmHotkey = &H312

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' An application sends this message to a window to allow changes in that window to be redrawn 
    ''' or to prevent changes in that window from being redrawn.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' The redraw state.
    ''' <para></para>
    ''' If this parameter is <see langword="True"/>, the content can be redrawn after a change.
    ''' <para></para>
    ''' If this parameter is <see langword="False"/>, the content cannot be redrawn after a change.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' This parameter is not used.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/dd145219%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmSetRedraw = &HB

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Sent to a window that the user is resizing.
    ''' <para></para>
    ''' By processing this message, an application can monitor the size and position of the drag rectangle
    ''' and, if needed, change its size or position.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' The edge of the window that is being sized.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' A pointer to a <see cref="Win32.Types.Rect"/> structure with the screen coordinates of the drag rectangle.
    ''' <para></para>
    ''' To change the size or position of the drag rectangle, an application must change the members of this structure.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms632647%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmSizing = &H214

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Sent one time to a window, after it enters the moving or sizing modal loop.
    ''' <para></para>
    ''' The window enters the moving or sizing modal loop when the user clicks the window's title bar or sizing border,
    ''' <para></para>
    ''' or when the window passes the <see cref="WindowsMessages.WmSysCommand"/> message to the 
    ''' <c>DefWindowProc</c> function and the <paramref name="wParam"/> parameter of the message
    ''' specifies the <see cref="Wparams.ScMove"/> or <see cref="Wparams.ScSize"/> value.
    ''' <para></para>
    ''' The operation is complete when <c>DefWindowProc</c> returns.
    ''' <para></para>
    ''' The system sends the <see cref="WmEnterSizeMove"/> message regardless of 
    ''' whether the dragging of full windows is enabled.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' This parameter is not used.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' This parameter is not used.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms632622%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmEnterSizeMove = &H231

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Sent one time to a window, after it has exited the moving or sizing modal loop.
    ''' <para></para>
    ''' The window enters the moving or sizing modal loop when the user clicks the window's title bar or sizing border,
    ''' <para></para>
    ''' or when the window passes the <see cref="WindowsMessages.WmSysCommand"/> message to the 
    ''' <c>DefWindowProc</c> function and the <paramref name="wParam"/> parameter of the message
    ''' specifies the <see cref="Wparams.ScMove"/> or <see cref="Wparams.ScSize"/> value.
    ''' <para></para>
    ''' The operation is complete when <c>DefWindowProc</c> returns.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' This parameter is not used.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' This parameter is not used.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms632623%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmExitSizeMove = &H232

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Sent to a window whose size, position, or place in the Z order is about to change as a 
    ''' result of a call to the <see cref="NativeMethods.SetWindowPos"/> function or another window-management function.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' This parameter is not used.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' A pointer to a <c>WINDOWPOS</c> structure that contains information about the window's new size and position.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms632653%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmWindowPosChanging = &H46

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' This message is posted to a window when the cursor is moved within the nonclient area of the window.
    ''' <para></para>
    ''' This message is posted to the window that contains the cursor.
    ''' <para></para>
    ''' If a window has captured the mouse this message is not posted.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' The hit-test value returned by the <c>DefWindowProc</c> function 
    ''' as a result of processing the <see cref="WindowsMessages.WmNchitTest"/> message.
    ''' <para></para>
    ''' For a list of hit-test values, see <see cref="WindowsMessages.WmNchitTest"/>.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' A <c>POINTS</c> structure that contains the x- and y-coordinates of the cursor.
    ''' <para></para>
    ''' The coordinates are relative to the upper-left corner of the screen. 
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms645627%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNcMouseMove = &HA0

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Posted to a window when the cursor moves.
    ''' <para></para>
    ''' If the mouse is not captured, the message is posted to the window that contains the cursor.
    ''' <para></para>
    ''' Otherwise, the message is posted to the window that has captured the mouse.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' Indicates whether various virtual keys are down.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' The low-order word specifies the x-coordinate of the cursor.
    ''' The coordinate is relative to the upper-left corner of the client area. 
    ''' <para></para>
    ''' The high-order word specifies the y-coordinate of the cursor.
    ''' The coordinate is relative to the upper-left corner of the client area.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms645616%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmMouseMove = &H200

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Sent to a window when the window is about to be hidden or shown.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' Indicates whether a window is being shown.
    ''' <para></para>
    ''' If wParam is <see langword="True"/>, the window is being shown.
    ''' If wParam is <see langword="False"/>, the window is being hidden.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' The status of the window being shown.
    ''' <para></para>
    ''' If <paramref name="lParam"/> is zero, the message was sent because of a 
    ''' call to the <see cref="NativeMethods.ShowWindow"/> function.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms645616%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmShowWindow = &H18

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Sent to a window after its size has changed.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' The type of resizing requested.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' The low-order word of <paramref name="lParam"/> specifies the new width of the client area.
    ''' <para></para>
    ''' The high-order word of <paramref name="lParam"/> specifies the new height of the client area. 
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms632646%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmSize = &H5

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent when a window is being activated or deactivated.
    ''' <para></para>
    ''' This message is sent first to the window procedure of the top-level window being deactivated; 
    ''' it is then sent to the window procedure of the top-level window being activated.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmActivate = &H6

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent when a window belonging to a different application than the 
    ''' active window is about to be activated. 
    ''' <para></para>
    ''' The message is sent to the application whose window is being activated and to 
    ''' the application whose window is being deactivated.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmActivateApp = &H1C

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' An application sends the message to indicate that the user interface (UI) state should be changed.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmChangeUiState = &H127

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message notifies a window that the user clicked the right mouse button (right-clicked) in the window.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmContextmenu = &H7B

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent when an application requests that a window be created by 
    ''' calling the <c>CreateWindowEx</c> or <c>CreateWindow</c> function.
    ''' <para></para>
    ''' (The message is sent before the function returns.) 
    ''' <para></para>
    ''' The window procedure of the new window receives this message after the window is 
    ''' created but before the window becomes visible.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmCreate = &H1

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent when a window is being destroyed.
    ''' <para></para>
    ''' It is sent to the window procedure of the window being destroyed after the 
    ''' window is removed from the screen.
    ''' <para></para>
    ''' This message is sent first to the window being destroyed and then 
    ''' to the child windows (if any) as they are destroyed.
    ''' <para></para>
    ''' During the processing of the message it can be assumed that all child windows still exist.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmDestroy = &H2

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to the clipboard owner when a call to the 
    ''' <c>EmptyClipboard</c> function empties the clipboard.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmDestroyClipboard = &H307

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Sent to the first window in the clipboard viewer chain when the content of the clipboard changes.
    ''' This enables a clipboard viewer window to display the new content of the clipboard.
    ''' <para></para>
    ''' A window receives this message through its WindowProc function.
    ''' <para></para>
    '''
    ''' <paramref name="wParam"/>
    ''' This parameter is not used and must be zero
    ''' <para></para>
    '''
    ''' <paramref name="lParam"/>
    ''' This parameter is not used and must be zero
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="https://docs.microsoft.com/en-us/windows/win32/dataxchg/wm-drawclipboard"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmDrawClipboard = &H308

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Sent to the first window in the clipboard viewer chain when a window is being removed from the chain.
    ''' <para></para>
    ''' A window receives this message through its WindowProc function.
    ''' <para></para>
    '''
    ''' <paramref name="wParam"/>
    ''' A handle to the window being removed from the clipboard viewer chain.
    ''' <para></para>
    '''
    ''' <paramref name="lParam"/>
    ''' A handle to the next window in the chain following the window being removed.
    ''' This parameter is NULL if the window being removed is the last window in the chain.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="https://docs.microsoft.com/en-us/windows/win32/dataxchg/wm-changecbchain"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmChangeCbChain = &H30D

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Notifies an application of a change to the hardware configuration of a device or the computer.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmDeviceChange = &H219

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to all top-level windows whenever the user changes device-mode settings.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmDevmodeChange = &H1B

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to all windows when the display resolution has changed.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmDisplayChange = &H7E

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent when an application changes the enabled state of a window.
    ''' It is sent to the window whose enabled state is changing.
    ''' <para></para>
    ''' This message is sent before the EnableWindow function returns but after the 
    ''' enabled state (<c>WS_DISABLED</c> style bit) of the window has changed.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmEnable = &HA

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to an application after the system processes the 
    ''' results of the <c>WM_QUERYENDSESSION</c> message. 
    ''' <para></para>
    ''' This message informs the application whether the session is ending.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmEndSession = &H16

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to the owner window of a modal dialog box or menu that is entering an idle state.
    ''' <para></para>
    ''' A modal dialog box or menu enters an idle state when no messages are waiting in its queue 
    ''' after it has processed one or more previous messages.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmEnterIdle = &H121

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent when the window background must be erased (for example when a window is resized).
    ''' <para></para>
    ''' The message is sent to prepare an invalidated portion of a window for painting.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmEraseBkgnd = &H14

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' An application sends the message to all top-level windows in the system after changing the 
    ''' pool of font resources.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmFontChange = &H1D

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' An application sends this message to determine the hot key associated with a window.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmGetHotkey = &H33

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to a window when the size or position of the window is about to change.
    ''' <para></para>
    ''' An application can use this message to override the window's default maximized size and 
    ''' position or its default minimum or maximum tracking size.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmGetMinMaxInfo = &H24

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Indicates that the user pressed the <c>F1</c> key.
    ''' <para></para>
    ''' If a menu is active when <c>F1</c> is pressed <see cref="WmHelp"/> is sent to the window associated with the menu; 
    ''' otherwise WmHELP is sent to the window that has the keyboard focus.
    ''' <para></para>
    ''' If no window has the keyboard focus <see cref="WmHelp"/> is sent to the currently active window.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmHelp = &H53

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' This message is sent to a window when a scroll event occurs in the window's standard horizontal scroll bar.
    ''' <para></para>
    ''' This message is also sent to the owner of a horizontal scroll bar control when a 
    ''' scroll event occurs in the control.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmHScroll = &H114

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to the dialog box procedure immediately before a dialog box is displayed.
    ''' <para></para>
    ''' Dialog box procedures typically use this message to initialize controls and carry out any other 
    ''' initialization tasks that affect the appearance of the dialog box.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmInitDialog = &H110

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted to the window with the keyboard focus when a nonsystem key is pressed.
    ''' <para></para>
    ''' A nonsystem key is a key that is pressed when the <c>ALT</c> key is not pressed.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmKeyDown = &H100

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted to the window with the keyboard focus when a nonsystem key is released.
    ''' <para></para>
    ''' A nonsystem key is a key that is pressed when the <c>ALT</c> key is not pressed 
    ''' or a keyboard key that is pressed when a window has the keyboard focus.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmKeyUp = &H101

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to a window immediately before it loses the keyboard focus.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmKillFocus = &H8

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted when the user double-clicks the left mouse button while the cursor is in the 
    ''' client area of a window.
    ''' <para></para>
    ''' If the mouse is not captured the message is posted to the window beneath the cursor. 
    ''' <para></para>
    ''' Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmLButtonDblClk = &H203

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted when the user presses the left mouse button while the cursor is in the 
    ''' client area of a window. 
    ''' <para></para>
    ''' If the mouse is not captured the message is posted to the window beneath the cursor. 
    ''' <para></para>
    ''' Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmLButtonDown = &H201

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted when the user releases the left mouse button while the cursor is in the 
    ''' client area of a window. 
    ''' <para></para>
    ''' If the mouse is not captured the message is posted to the window beneath the cursor. 
    ''' <para></para>
    ''' Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmLButtonUp = &H202

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The WmMBUTTONDBLCLK message is posted when the user double-clicks the middle mouse button while the 
    ''' cursor is in the client area of a window.
    ''' <para></para>
    ''' If the mouse is not captured the message is posted to the window beneath the cursor.
    ''' <para></para>
    ''' Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmMButtonDblClk = &H209

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted when the user presses the middle mouse button while the cursor is in the 
    ''' client area of a window.
    ''' <para></para>
    ''' If the mouse is not captured the message is posted to the window beneath the cursor.
    ''' <para></para>
    ''' Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmMButtonDown = &H207

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted when the user releases the middle mouse button while the cursor is in the 
    ''' client area of a window. 
    ''' <para></para>
    ''' If the mouse is not captured the message is posted to the window beneath the cursor. 
    ''' <para></para>
    ''' Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmMButtonUp = &H208

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' An application sends this message to a multiple-document interface (MDI) client window to 
    ''' instruct the client window to activate a different MDI child window.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmMdiActivate = &H222

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' An application sends this message to a multiple-document interface (MDI) client window to 
    ''' create an MDI child window.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmMdiCreate = &H220

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' An application sends this message to a multiple-document interface (MDI) client window to 
    ''' close an MDI child window.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmMdiDestroy = &H221

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent when the user makes a selection from a menu.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmMenuCommand = &H126

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent when the user releases the right mouse button while the cursor is on a menu item.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmMenuRButtonUp = &H122

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to a menu's owner window when the user selects a menu item.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmMenuSelect = &H11F

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent when the cursor is in an inactive window and the user presses a mouse button.
    ''' <para></para>
    ''' The parent window receives this message only if the child window passes it to the <c>DefWindowProc</c> function.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmMouseActivate = &H21

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted to a window when the cursor hovers over the client area of the window for the 
    ''' period of time specified in a prior call to <c>TrackMouseEvent</c>.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmMouseHover = &H2A1

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted to a window when the cursor leaves the client area of the 
    ''' window specified in a prior call to <c>TrackMouseEvent</c>.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmMouseLeave = &H2A3

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to the focus window when the mouse wheel is rotated.
    ''' <para></para>
    ''' The <c>DefWindowProc</c> function propagates the message to the window's parent. 
    ''' <para></para>
    ''' There should be no internal forwarding of the message since <c>DefWindowProc</c> propagates it up the 
    ''' parent chain until it finds a window that processes it.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmMouseWheel = &H20A

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to the focus window when the mouse's horizontal scroll wheel is tilted or rotated.
    ''' <para></para>
    ''' The <c>DefWindowProc</c> function propagates the message to the window's parent.
    ''' <para></para>
    ''' There should be no internal forwarding of the message since <c>DefWindowProc</c> propagates it up 
    ''' the parent chain until it finds a window that processes it.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmMouseHWheel = &H20E

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to a window that the user is moving.
    ''' <para></para>
    ''' By processing this message an application can monitor the position of the drag rectangle and
    '''  if needed change its position.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmMoving = &H216

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Non Client Area Activated Caption(Title) of the Form.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNcActivate = &H86

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent when the size and position of a window's client area must be calculated.
    ''' <para></para>
    ''' By processing this message an application can control the content of the window's client area 
    ''' when the size or position of the window changes.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNcCalcSize = &H83

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent prior to the <see cref="WmCreate"/> message when a window is first created.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNcCreate = &H81

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message informs a window that its nonclient area is being destroyed.
    ''' <para></para>
    ''' The <c>DestroyWindow</c> function sends the <see cref="WmNcDestroy"/> message to the 
    ''' window following the <see cref="WmDestroy"/> message.
    ''' <para></para>
    ''' <see cref="WmDestroy"/> is used to free the allocated memory object associated with the window.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNcDestroy = &H82

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted when the user double-clicks the left mouse button while the cursor is 
    ''' within the nonclient area of a window.
    ''' <para></para>
    ''' This message is posted to the window that contains the cursor.
    ''' <para></para>
    ''' If a window has captured the mouse this message is not posted.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNcLButtonDblClk = &HA3

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted when the user double-clicks the middle mouse button while the cursor is 
    ''' within the nonclient area of a window.
    ''' <para></para>
    ''' This message is posted to the window that contains the cursor. 
    ''' <para></para>
    ''' If a window has captured the mouse this message is not posted.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNcMButtonDblClk = &HA9

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted when the user presses the middle mouse button while the cursor is 
    ''' within the nonclient area of a window. 
    ''' <para></para>
    ''' This message is posted to the window that contains the cursor. 
    ''' <para></para>
    ''' If a window has captured the mouse this message is not posted.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNcMButtonDown = &HA7

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted when the user releases the middle mouse button while the cursor is 
    ''' within the nonclient area of a window.
    ''' <para></para>
    ''' This message is posted to the window that contains the cursor. 
    ''' <para></para>
    ''' If a window has captured the mouse this message is not posted.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNcMButtonUp = &HA8

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted to a window when the cursor leaves the nonclient area of the 
    ''' window specified in a prior call to <c>TrackMouseEvent</c>.
    ''' </summary>
    WmNcMouseLeave = &H2A2

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to a window when its frame must be painted.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNcPaint = &H85

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted when the user double-clicks the right mouse button while the cursor is 
    ''' within the nonclient area of a window.
    ''' <para></para>
    ''' This message is posted to the window that contains the cursor.
    ''' <para></para>
    ''' If a window has captured the mouse this message is not posted.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNcRButtonDblClk = &HA6

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Occurs when the control needs repainting.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmPaint = &HF

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Notifies applications that a power-management event has occurred.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmPowerBroadcast = &H218

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to a window to request that it draw itself in the specified device context
    '''  most commonly in a printer device context.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmPrint = &H317

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to a window to request that it draw its client area in the specified device context 
    ''' most commonly in a printer device context.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmPrintClient = &H318

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent when the user chooses to end the session or when an application calls one of the 
    ''' system shutdown functions.
    ''' <para></para>
    ''' If any application returns zero the session is not ended.
    ''' <para></para>
    ''' The system stops sending <see cref="WmQueryEndSession"/> messages as soon as one application returns zero.
    ''' <para></para>
    ''' After processing this message the system sends the <see cref="WmEndSession"/> message with the 
    ''' <paramref name="wParam"/> parameter set to the results of the <see cref="WmQueryEndSession"/> message.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmQueryEndSession = &H11

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Once received it ends the application's Message Loop signaling the application to end.
    ''' <para></para>
    ''' It can be sent by pressing <c>Alt</c>+<c>F4</c> Clicking the X in the upper right-hand of the 
    ''' program or going to File->Exit.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmQuit = &H12

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted when the user double-clicks the right mouse button while the cursor is in the 
    ''' client area of a window.
    ''' <para></para>
    ''' If the mouse is not captured the message is posted to the window beneath the cursor.
    ''' <para></para>
    ''' Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmRButtonDblClk = &H206

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted when the user presses the right mouse button while the cursor is in the 
    ''' client area of a window.
    ''' <para></para>
    ''' If the mouse is not captured the message is posted to the window beneath the cursor.
    ''' <para></para>
    ''' Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmRButtonDown = &H204

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted when the user releases the right mouse button while the cursor is in the 
    ''' client area of a window.
    ''' <para></para>
    ''' If the mouse is not captured the message is posted to the window beneath the cursor.
    ''' <para></para>
    ''' Otherwise the message is posted to the window that has captured the mouse.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmRButtonUp = &H205

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' When the control got the focus.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmSetFocus = &H7

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' An application sends this message to a window to associate a hot key with the window.
    ''' <para></para>
    ''' When the user presses the hot key the system activates the window.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmSetHotkey = &H32

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent from Print Manager whenever a job is added to or removed from the Print Manager queue.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmSpoolerStatus = &H2A

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to a window after the <c>SetWindowLong</c> function has changed one or more of the window's styles.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmStyleChanged = &H7D

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to a window when the <c>SetWindowLong</c> function is about to change one or more of the 
    ''' window's styles.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmStyleChanging = &H7C

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' This message is sent to all top-level windows when a change is made to a system color setting.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmSysColorChange = &H15

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted to the window with the keyboard focus when the user presses the <c>F10</c> key 
    ''' (which activates the menu bar) or holds down the <c>ALT</c> key and then presses another key.
    ''' <para></para>
    ''' It also occurs when no window currently has the keyboard focus; 
    ''' in this case the <see cref="WmSysKeyDown"/> message is sent to the active window.
    ''' <para></para>
    ''' The window that receives the message can distinguish between these two contexts by checking the 
    ''' context code in the <paramref name="lParam"/> parameter.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmSysKeyDown = &H104

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is posted to the window with the keyboard focus when the user releases a key that 
    ''' was pressed while the <c>ALT</c> key was held down.
    ''' <para></para>
    ''' It also occurs when no window currently has the keyboard focus; 
    ''' in this case the <see cref="WmSysKeyUp"/> message is sent to the active window.
    ''' <para></para>
    ''' The window that receives the message can distinguish between these two contexts by checking the 
    ''' context code in the <paramref name="lParam"/> parameter.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmSysKeyUp = &H105

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' A message that is sent whenever there is a change in the system time.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmTimeChange = &H1E

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' An application sends this message to an edit control to undo the last operation.
    ''' <para></para>
    ''' When this message is sent to an edit control the previously deleted text is restored or the 
    ''' previously added text is deleted.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmUndo = &H304

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to all windows after the user has logged on or off.
    ''' <para></para>
    ''' When the user logs on or off the system updates the user-specific settings.
    ''' <para></para>
    ''' The system sends this message immediately after updating the settings.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmUserChanged = &H54

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to a window when a scroll event occurs in the window's standard vertical scroll bar.
    ''' <para></para>
    ''' This message is also sent to the owner of a vertical scroll bar control when a scroll event occurs in the control.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmVScroll = &H115

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' The message is sent to a window whose size position or place in the Z order has changed as a 
    ''' result of a call to the <c>SetWindowPos</c> function or another window-management function.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href=""/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmWindowPosChanged = &H47

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' An application sends this message to an edit control or combo box to copy the current 
    ''' selection to the clipboard in <c>CF_TEXT</c> format.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' This parameter is not used and must be zero.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' This parameter is not used and must be zero.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="https://msdn.microsoft.com/en-us/library/windows/desktop/ms649022%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmCopy = &H301

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' An application sends this message to an edit control or combo box to delete (cut) the 
    ''' current selection if any in the edit control and copy the deleted text to the clipboard in <c>CF_TEXT</c> format.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' This parameter is not used and must be zero.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' This parameter is not used and must be zero.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="https://msdn.microsoft.com/en-us/library/windows/desktop/ms649023%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmCut = &H300

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' An application sends this message to an edit control or combo box to copy the current content of the 
    ''' clipboard to the edit control at the current caret position.
    ''' <para></para>
    ''' Data is inserted only if the clipboard contains data in <c>CF_TEXT</c> format.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' This parameter is not used and must be zero.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' This parameter is not used and must be zero.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="https://msdn.microsoft.com/en-us/library/windows/desktop/ms649028%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmPaste = &H302

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' An application sends the message to an edit control or combo box to delete (clear) the 
    ''' current selection if any from the edit control.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' This parameter is not used and must be zero.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' This parameter is not used and must be zero.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="https://msdn.microsoft.com/en-us/library/windows/desktop/ms649020%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmClear = &H303

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Posted when the user presses the first or second X button while the cursor is in the client area of a window.
    ''' <para></para>
    ''' If the mouse is not captured, the message is posted to the window beneath the cursor.
    ''' <para></para>
    ''' Otherwise, the message is posted to the window that has captured the mouse.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' The low-order word indicates whether various virtual keys are down.
    ''' <para></para>
    ''' The high-order word indicates which button was clicked.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' The low-order word specifies the x-coordinate of the cursor. 
    ''' The coordinate is relative to the upper-left corner of the client area.
    ''' <para></para>
    ''' The high-order word specifies the y-coordinate of the cursor. 
    ''' The coordinate is relative to the upper-left corner of the client area.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="https://msdn.microsoft.com/en-us/library/windows/desktop/ms646245%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmXButtonDown = &H20B

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Posted when the user releases the first or second X button while the cursor is in the client area of a window.
    ''' <para></para>
    ''' If the mouse is not captured, the message is posted to the window beneath the cursor.
    ''' <para></para>
    ''' Otherwise, the message is posted to the window that has captured the mouse.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' The low-order word indicates whether various virtual keys are down.
    ''' <para></para>
    ''' The high-order word indicates which button was double-clicked.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' The low-order word specifies the x-coordinate of the cursor. 
    ''' The coordinate is relative to the upper-left corner of the client area.
    ''' <para></para>
    ''' The high-order word specifies the y-coordinate of the cursor. 
    ''' The coordinate is relative to the upper-left corner of the client area.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="https://msdn.microsoft.com/en-us/library/windows/desktop/ms646246%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmXButtonUp = &H20C

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Posted when the user double-clicks the first or second X button while the cursor is in the client area of a window.
    ''' <para></para>
    ''' If the mouse is not captured, the message is posted to the window beneath the cursor.
    ''' <para></para>
    ''' Otherwise, the message is posted to the window that has captured the mouse.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' The low-order word indicates whether various virtual keys are down.
    ''' <para></para>
    ''' The high-order word indicates which button was double-clicked.
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' The low-order word specifies the x-coordinate of the cursor. 
    ''' The coordinate is relative to the upper-left corner of the client area.
    ''' <para></para>
    ''' The high-order word specifies the y-coordinate of the cursor. 
    ''' The coordinate is relative to the upper-left corner of the client area.
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="https://msdn.microsoft.com/en-us/library/windows/desktop/ms646244%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmXButtonDblClk = &H20D

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Posted when the user presses the first or second X button while the cursor is in the client area of a window.
    ''' <para></para>
    ''' If the mouse is not captured, the message is posted to the window beneath the cursor.
    ''' <para></para>
    ''' Otherwise, the message is posted to the window that has captured the mouse.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' The low-order word specifies the hit-test value returned by the 
    ''' <c>DefWindowProc</c> function from processing the <see cref="WmNchitTest"/> message. 
    ''' <para></para>
    ''' For a list of hit-test values, <see cref="WmNchitTest"/>.
    ''' <para></para>
    ''' The high-order word indicates which button was pressed. 
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' A pointer to a <c>POINTS</c> structure that contains the x- and y-coordinates of the cursor.
    ''' <para></para>
    ''' The coordinates are relative to the upper-left corner of the screen. 
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="https://msdn.microsoft.com/en-us/library/windows/desktop/ms645632%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNcXButtonDown = &HAB

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Posted when the user releases the first or second X button while the cursor is in the nonclient area of a window.
    ''' <para></para>
    ''' This message is posted to the window that contains the cursor.
    ''' <para></para>
    ''' If a window has captured the mouse, this message is not posted.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' The low-order word specifies the hit-test value returned by the 
    ''' <c>DefWindowProc</c> function from processing the <see cref="WmNchitTest"/> message. 
    ''' <para></para>
    ''' For a list of hit-test values, <see cref="WmNchitTest"/>.
    ''' <para></para>
    ''' The high-order word indicates which button was released. 
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' A pointer to a <c>POINTS</c> structure that contains the x- and y-coordinates of the cursor.
    ''' <para></para>
    ''' The coordinates are relative to the upper-left corner of the screen. 
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="https://msdn.microsoft.com/en-us/library/windows/desktop/ms646240%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNcXButtonUp = &HAC

    ''' ----------------------------------------------------------------------------------------------------
    ''' <summary>
    ''' Posted when the user double-clicks the first or second X button while the cursor is in the nonclient area of a window.
    ''' <para></para>
    ''' This message is posted to the window that contains the cursor.
    ''' <para></para>
    ''' If a window has captured the mouse, this message is not posted.
    ''' <para></para>
    ''' 
    ''' <paramref name="wParam"/> 
    ''' The low-order word specifies the hit-test value returned by the 
    ''' <c>DefWindowProc</c> function from processing the <see cref="WmNchitTest"/> message. 
    ''' <para></para>
    ''' For a list of hit-test values, <see cref="WmNchitTest"/>.
    ''' <para></para>
    ''' The high-order word indicates which button was double-clicked. 
    ''' <para></para>
    ''' 
    ''' <paramref name="lParam"/> 
    ''' A pointer to a <c>POINTS</c> structure that contains the x- and y-coordinates of the cursor.
    ''' <para></para>
    ''' The coordinates are relative to the upper-left corner of the screen. 
    ''' </summary>
    ''' ----------------------------------------------------------------------------------------------------
    ''' <remarks>
    ''' <see href="https://msdn.microsoft.com/en-us/library/windows/desktop/ms645631%28v=vs.85%29.aspx"/>
    ''' </remarks>
    ''' ----------------------------------------------------------------------------------------------------
    WmNcXButtonDblClk = &HAD

    End Enum
```

## Example - C# - sivakumar.keerthi
```cs
using System;
using System.Drawing;
using System.Collections;
using System.ComponentModel;
using System.Windows.Forms;
using System.Data;
using System.Runtime.InteropServices;

namespace WindowsApplication1
{
    /// <summary>
    /// Summary description for Form1.
    /// </summary>
    public class Form1 : System.Windows.Forms.Form
    {
        /// <summary>
        /// Required designer variable.
        /// </summary>
        [DllImport("user32.dll")]
        private static extern IntPtr GetSystemMenu(IntPtr hWnd, bool bRevert);
        [DllImport("user32.dll")]
        private static extern bool InsertMenu (IntPtr hMenu, Int32 wPosition, Int32 wFlags, Int32 wIDNewItem, string lpNewItem);

        public const Int32 WM_SYSCOMMAND = 0x112;
        public const Int32 MF_SEPARATOR = 0x800;
        public const Int32 MF_BYPOSITION = 0x400;
        public const Int32 MF_STRING = 0x0;
        public const Int32 MenuItem1  = 1000;
        public const Int32 MenuItem2 = 1001;
        public const Int32 WM_CLOSE = 0xF060;

        private System.ComponentModel.Container components = null;

        public Form1()
        {
            //
            // Required for Windows Form Designer support
            //
            InitializeComponent();
            //
            // TODO: Add any constructor code after InitializeComponent call
            //
        }

        /// <summary>
        /// Clean up any resources being used.
        /// </summary>
        protected override void Dispose( bool disposing )
        {
            if( disposing )
            {
                if (components != null) 
                {
                    components.Dispose();
                }
            }
            base.Dispose( disposing );
        }

        #region Windows Form Designer generated code
        /// <summary>
        /// Required method for Designer support - do not modify
        /// the contents of this method with the code editor.
        /// </summary>
        private void InitializeComponent()
        {
            // 
            // Form1
            // 
            this.AutoScaleBaseSize = new System.Drawing.Size(5, 13);
            this.ClientSize = new System.Drawing.Size(528, 266);
            this.Name = "Form1";
            this.Text = "Form1";
            this.Load += new System.EventHandler(this.Form1_Load);

        }
        #endregion

        /// <summary>
        /// The main entry point for the application.
        /// </summary>
        [STAThread]
        static void Main() 
        {
            Application.Run(new Form1());
        }

        protected override void WndProc(ref Message m)
        {
            if(m.Msg == WM_SYSCOMMAND)
            {
                switch(m.WParam.ToInt32())
                {
                    case MenuItem1:
                        MessageBox.Show("Clicked MenuItem1");
                        return;
                    case MenuItem2:
                        MessageBox.Show("Clicked MenuItem2");
                        return;
                    case WM_CLOSE:
                        MessageBox.Show("Can't Close");
                        return;
                    default:
                        break;
                } 
            }
            base.WndProc(ref m);
        }

        private void Form1_Load(object sender, System.EventArgs e)
        {
            IntPtr sysMenuHandle = GetSystemMenu(this.Handle, false);
            InsertMenu(sysMenuHandle, 5, MF_BYPOSITION |MF_SEPARATOR, 0, string.Empty);
            InsertMenu(sysMenuHandle, 6, MF_BYPOSITION , MenuItem1, "MenuItem1");
            InsertMenu(sysMenuHandle, 7, MF_BYPOSITION , MenuItem2, "MenuItem2");
        }
    }
}
Enumeration for supporting the wParam parameter included with the WM_SIZING notification.  Check with WindowsMessages for more details.1/13/2008 2:31:03 AM - dj_elektrona@abv.bg-84.238.190.222The return value of the DefWindowProc function, indicating the position of the cursor hot spot.  These values can also be used within WndProc(ref Message) implementations when authoring classes that inherit from Control or Form objects in .NET WinForms applications.7/31/2021 4:40:32 PM - Carter N-108.172.185.64
```
