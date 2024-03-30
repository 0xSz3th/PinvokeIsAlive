
## C# Signature:
```cs
/// <summary>
/// Sets the show state and the restored, minimized, and maximized positions of the specified window.
/// </summary>
/// <param name="hWnd">
/// A handle to the window.
/// </param>
/// <param name="lpwndpl">
/// A pointer to a WINDOWPLACEMENT structure that specifies the new show state and window positions.
/// <para>
/// Before calling SetWindowPlacement, set the length member of the WINDOWPLACEMENT structure to sizeof(WINDOWPLACEMENT). SetWindowPlacement fails if the length member is not set correctly.
/// </para>
/// </param>
/// <returns>
/// If the function succeeds, the return value is nonzero.
/// <para>
/// If the function fails, the return value is zero. To get extended error information, call GetLastError.
/// </para>
/// </returns>
[DllImport("user32.dll", SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool SetWindowPlacement(IntPtr hWnd,
   [In] ref WINDOWPLACEMENT lpwndpl);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Public Shared Function SetWindowPlacement( _
     ByVal hWnd As IntPtr, _
     ByRef lpwndpl As WINDOWPLACEMENT) As Boolean
End Function
```

## VB Signature
```cs
Public Declare Function SetWindowPlacement Lib "user32" _
         (ByVal hWnd As Long, _
          ByRef lpwndpl As WINDOWPLACEMENT) As Long
```

## Sample Code:
```cs
private void GetPlacement()
{
        WINDOWPLACEMENT placement = new WINDOWPLACEMENT();
        placement.length = Marshal.SizeOf(placement);
        GetWindowPlacement(this.Handle, ref placement);
}
```
