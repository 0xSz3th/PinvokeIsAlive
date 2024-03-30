
## C# Signature:
```cs
/// <summary>
///     Retrieves the length, in characters, of the specified window's title bar text (if the window has a title bar). If
///     the specified window is a control, the function retrieves the length of the text within the control. However,
///     GetWindowTextLength cannot retrieve the length of the text of an edit control in another application.
///     <para>
///     Go to https://msdn.microsoft.com/en-us/library/windows/desktop/ms633521%28v=vs.85%29.aspx for more
///     information
///     </para>
/// </summary>
/// <param name="hWnd">C++ ( hWnd [in]. Type: HWND )<br />A <see cref="IntPtr" /> handle to the window or control.</param>
/// <returns>
///     If the function succeeds, the return value is the length, in characters, of the text. Under certain
///     conditions, this value may actually be greater than the length of the text.<br />For more information, see the
///     following Remarks section. If the window has no text, the return value is zero.To get extended error information,
///     call GetLastError.
/// </returns>
/// <remarks>
///     If the target window is owned by the current process, <see cref="GetWindowTextLength" /> causes a
///     WM_GETTEXTLENGTH message to be sent to the specified window or control.<br />Under certain conditions, the
///     <see cref="GetWindowTextLength" /> function may return a value that is larger than the actual length of the
///     text.This occurs with certain mixtures of ANSI and Unicode, and is due to the system allowing for the possible
///     existence of double-byte character set (DBCS) characters within the text. The return value, however, will always be
///     at least as large as the actual length of the text; you can thus always use it to guide buffer allocation. This
///     behavior can occur when an application uses both ANSI functions and common dialogs, which use Unicode.It can also
///     occur when an application uses the ANSI version of <see cref="GetWindowTextLength" /> with a window whose window
///     procedure is Unicode, or the Unicode version of <see cref="GetWindowTextLength" /> with a window whose window
///     procedure is ANSI.<br />For more information on ANSI and ANSI functions, see Conventions for Function Prototypes.
///     <br />To obtain the exact length of the text, use the WM_GETTEXT, LB_GETTEXT, or CB_GETLBTEXT messages, or the
///     GetWindowText function.
/// </remarks>
[DllImport("user32.dll", SetLastError=true, CharSet=CharSet.Auto)]
static extern int GetWindowTextLength(IntPtr hWnd);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", SetLastError:=True, CharSet:=CharSet.Auto)> _
Private Shared Function GetWindowTextLength(ByVal hwnd As IntPtr) As Integer
End Function
```

## Oxygene.NET Signature:
```cs
[DllImport("user32.dll", SetLastError := true, CharSet := CharSet.Auto)]
class method GetWindowTextLength(hWnd: IntPtr): Int32; external;
```

## VB Signature:
```cs
Public Declare Function GetWindowTextLength Lib "user32.dll" Alias "GetWindowTextLengthA" _
         (ByVal hWnd As Long) As Long
```
