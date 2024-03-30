
## C# Signature:
```cs
[DllImport("user32.dll")]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool FlashWindowEx(ref FLASHWINFO pwfi);
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct FLASHWINFO
{
    public UInt32 cbSize;
    public IntPtr hwnd;
    public UInt32 dwFlags;
    public UInt32 uCount;
    public UInt32 dwTimeout;
}

public enum FlashWindow : uint
    {
    /// <summary>
    /// Stop flashing. The system restores the window to its original state. 
    /// </summary>    
    FLASHW_STOP = 0,

    /// <summary>
    /// Flash the window caption 
    /// </summary>
    FLASHW_CAPTION = 1,

    /// <summary>
    /// Flash the taskbar button. 
    /// </summary>
    FLASHW_TRAY = 2,

    /// <summary>
    /// Flash both the window caption and taskbar button.
    /// This is equivalent to setting the FLASHW_CAPTION | FLASHW_TRAY flags. 
    /// </summary>
    FLASHW_ALL = 3,

    /// <summary>
    /// Flash continuously, until the FLASHW_STOP flag is set.
    /// </summary>
    FLASHW_TIMER = 4,

    /// <summary>
    /// Flash continuously until the window comes to the foreground. 
    /// </summary>
    FLASHW_TIMERNOFG = 12
    }
```

## Sample Code:
```cs
/// <summary>
/// Flashes a window
/// </summary>
/// <param name="hWnd">The handle to the window to flash</param>
/// <returns>whether or not the window needed flashing</returns>
public static bool FlashWindowEx(IntPtr hWnd)
{
    FLASHWINFO fInfo = new FLASHWINFO();

    fInfo.cbSize = Convert.ToUInt32(Marshal.SizeOf(fInfo));
    fInfo.hwnd = hWnd;
    fInfo.dwFlags = FLASHW_ALL;
    fInfo.uCount = UInt32.MaxValue;
    fInfo.dwTimeout = 0;

    return FlashWindowEx(ref fInfo);
}
```

## Sample Code:
```cs
/// Minor adjust to the code above
/// <summary>
/// Flashes a window until the window comes to the foreground
/// Receives the form that will flash
/// </summary>
/// <param name="hWnd">The handle to the window to flash</param>
/// <returns>whether or not the window needed flashing</returns>
public static bool FlashWindowEx(Form frm)
{
        IntPtr hWnd = frm.Handle;
        FLASHWINFO fInfo = new FLASHWINFO();

        fInfo.cbSize = Convert.ToUInt32(Marshal.SizeOf(fInfo));
        fInfo.hwnd = hWnd;
        fInfo.dwFlags = FLASHW_ALL | FLASHW_TIMERNOFG;
        fInfo.uCount = UInt32.MaxValue;
        fInfo.dwTimeout = 0;

        return FlashWindowEx(ref fInfo);
}
```

## Alternative Managed API:
```cs
Private Declare Function FlashWindowEx Lib "User32.dll" (ByRef fwInfo As FLASHWINFO) As Boolean

    ' As defined by: http://msdn.microsoft.com/en-us/library/ms679347(v=vs.85).aspx
    Public Enum FlashWindowFlags As UInteger
    ' Stop flashing. The system restores the window to its original state.
    FLASHW_STOP = 0
    ' Flash the window caption.
    FLASHW_CAPTION = 1
    ' Flash the taskbar button.
    FLASHW_TRAY = 2
    ' Flash both the window caption and taskbar button.
    ' This is equivalent to setting the FLASHW_CAPTION | FLASHW_TRAY flags.
    FLASHW_ALL = 3
    ' Flash continuously, until the FLASHW_STOP flag is set.
    FLASHW_TIMER = 4
    ' Flash continuously until the window comes to the foreground.
    FLASHW_TIMERNOFG = 12
    End Enum

    Public Structure FLASHWINFO
    Public cbSize As UInteger
    Public hwnd As UInteger
    Public dwFlags As FlashWindowFlags
    Public uCount As UInteger
    Public dwTimeout As UInteger
    End Structure

    Public Function FlashWindow(ByRef frm As Windows.Forms.Form) As Boolean
    Return FlashWindow(frm, True, True, 5)
    End Function
    Public Function FlashWindow(ByRef frm As Windows.Forms.Form, ByVal FlashTitleBar As Boolean, ByVal FlashTray As Boolean) As Boolean
    Return FlashWindow(frm, FlashTitleBar, FlashTray, 5)
    End Function
    Public Function FlashWindow(ByRef frm As Windows.Forms.Form, ByVal FlashCount As Integer) As Boolean
    Return FlashWindow(frm, True, True, FlashCount)
    End Function
    Public Function FlashWindow(ByRef frm As Windows.Forms.Form, ByVal FlashTitleBar As Boolean, ByVal FlashTray As Boolean, ByVal FlashCount As Integer) As Boolean
    If frm Is Nothing Then Return False
    If frm.IsDisposed Then Return False
    If frm.Handle = 0 Then Return False

    Try
        Dim fwi As New FLASHWINFO
        With fwi
        .hwnd = frm.Handle
        If FlashTitleBar Then .dwFlags = .dwFlags Or FlashWindowFlags.FLASHW_CAPTION
        If FlashTray Then .dwFlags = .dwFlags Or FlashWindowFlags.FLASHW_TRAY
        .uCount = FlashCount
        If FlashCount = 0 Then .dwFlags = .dwFlags Or FlashWindowFlags.FLASHW_TIMERNOFG
        .dwTimeout = 0 ' Use the default cursor blink rate.
        .cbSize = System.Runtime.InteropServices.Marshal.SizeOf(fwi)
        End With

        Return FlashWindowEx(fwi)
    Catch
        Return False
    End Try
    End Function
```
