
## C# Signature:
```cs
/// <summary>
/// Retrieves a handle to a window that has the specified relationship (Z-Order or owner) to the specified window.
/// </summary>
/// <remarks>The EnumChildWindows function is more reliable than calling GetWindow in a loop. An application that
/// calls GetWindow to perform this task risks being caught in an infinite loop or referencing a handle to a window
/// that has been destroyed.</remarks>
/// <param name="hWnd">A handle to a window. The window handle retrieved is relative to this window, based on the
/// value of the uCmd parameter.</param>
/// <param name="uCmd">The relationship between the specified window and the window whose handle is to be
/// retrieved.</param>
/// <returns>
/// If the function succeeds, the return value is a window handle. If no window exists with the specified relationship
/// to the specified window, the return value is NULL. To get extended error information, call GetLastError.
/// </returns>
[DllImport("user32.dll", SetLastError = true)]
private static extern IntPtr GetWindow(IntPtr hWnd, GetWindowType uCmd);

private enum GetWindowType : uint
{
     /// <summary>
     /// The retrieved handle identifies the window of the same type that is highest in the Z order.
     /// <para/>
     /// If the specified window is a topmost window, the handle identifies a topmost window.
     /// If the specified window is a top-level window, the handle identifies a top-level window.
     /// If the specified window is a child window, the handle identifies a sibling window.
     /// </summary>
     GW_HWNDFIRST = 0,
     /// <summary>
     /// The retrieved handle identifies the window of the same type that is lowest in the Z order.
     /// <para />
     /// If the specified window is a topmost window, the handle identifies a topmost window.
     /// If the specified window is a top-level window, the handle identifies a top-level window.
     /// If the specified window is a child window, the handle identifies a sibling window.
     /// </summary>
     GW_HWNDLAST = 1,
     /// <summary>
     /// The retrieved handle identifies the window below the specified window in the Z order.
     /// <para />
     /// If the specified window is a topmost window, the handle identifies a topmost window.
     /// If the specified window is a top-level window, the handle identifies a top-level window.
     /// If the specified window is a child window, the handle identifies a sibling window.
     /// </summary>
     GW_HWNDNEXT = 2,
     /// <summary>
     /// The retrieved handle identifies the window above the specified window in the Z order.
     /// <para />
     /// If the specified window is a topmost window, the handle identifies a topmost window.
     /// If the specified window is a top-level window, the handle identifies a top-level window.
     /// If the specified window is a child window, the handle identifies a sibling window.
     /// </summary>
     GW_HWNDPREV = 3,
     /// <summary>
     /// The retrieved handle identifies the specified window's owner window, if any.
     /// </summary>
     GW_OWNER = 4,
     /// <summary>
     /// The retrieved handle identifies the child window at the top of the Z order,
     /// if the specified window is a parent window; otherwise, the retrieved handle is NULL.
     /// The function examines only child windows of the specified window. It does not examine descendant windows.
     /// </summary>
     GW_CHILD = 5,
     /// <summary>
     /// The retrieved handle identifies the enabled popup window owned by the specified window (the
     /// search uses the first such window found using GW_HWNDNEXT); otherwise, if there are no enabled
     /// popup windows, the retrieved handle is that of the specified window.
     /// </summary>
     GW_ENABLEDPOPUP = 6
}
```

## VB Signature:
```cs
Declare Auto Function GetWindow Lib "user32.dll" ( _
   ByVal hWnd As IntPtr, ByVal uCmd As UInt32) As IntPtr
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", SetLastError:=True, CharSet:=CharSet.Auto)> _
    Private Shared Function GetWindow(ByVal hWnd As IntPtr, ByVal uCmd As UInt32) As IntPtr
    End Function

Private Enum GetWindowType As UInteger
    GW_HWNDFIRST = 0
    GW_HWNDLAST = 1
    GW_HWNDNEXT = 2
    GW_HWNDPREV = 3
    GW_OWNER = 4
    GW_CHILD = 5
    GW_ENABLEDPOPUP = 6
End Enum
```

## Tips & Tricks:
```cs
' (VB.NET): Get the owner of a program. Sometimes works better than using .GetParent. (i.e. when using .GetParent on the Desktop it would return no hWnd; this will return one.)
Dim Owner As IntPtr = GetWindow(hWnd, GW_OWNER)
```

## Sample Code:
```cs
// Get the handle to a dialog
IntPtr dlgHandle = GetWindow(myProcess.MainWindowHandle, GW_ENABLEDPOPUP);
```
