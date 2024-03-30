
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool InvalidateRect(IntPtr hWnd, IntPtr lpRect, bool bErase);
```

## VB Signature:
```cs
Public Overloads Declare Function InvalidateRect Lib "User32" Alias "InvalidateRect" (ByVal hWnd As Int32, ByRef lpRect As RECT, ByVal bErase As Boolean) As Boolean
Public Overloads Declare Function InvalidateRect Lib "User32" Alias "InvalidateRect" (ByVal hWnd As Int32, ByVal lpRect As IntPtr, ByVal bErase As Boolean) As Boolean
Public Overloads Shared Function InvalidateRect(ByVal hWnd As Int32, ByVal bErase As Boolean) As Boolean
     Return InvalidateRect(hWnd, IntPtr.Zero, bErase)
End Function
Public Overloads Shared Function InvalidateRect(ByVal hWnd As Int32, ByVal lpRect As System.Drawing.Rectangle, ByVal bErase As Boolean) As Boolean
     Return InvalidateRect(hWnd, RECT.FromRectangle(lpRect), bErase)
End Function
```

## Sample Code:
```cs
POINT pt;
RECT rct;
/** converted coords **/
Rectangle R;

/** get current current cursor location **/
GetCursorPos(out pt)

/** get the window handle **/
IntPtr hWnd = WindowFromPoint(pt);
GetWindowRect(hWnd, out rct);

/** draw a red border around your rectangle **/
ControlPaint.DrawBorder(System.Drawing.Graphics.FromHwnd(hWnd), R, Color.Red, ButtonBorderStyle.Solid);

/** when you want to clear this rectangle, use this **/
InvalidateRect(hWnd, IntPtr.Zero, true);
```

## Alternative Managed API:
```cs
Invalidate method
Invalidate() - invalidates the entire surface causing the control to be repainted.
Invalidate(bool invalidateChilden) - Optionally, invalidates the child controls assigned to the control.
Invalidate(Rectangle rect) - Adds the specified rectangle to the update region of the control
                and causes a paint message to be sent to the control.
Invalidate(Rectangle rect, bool invalidateChildern) - combination of the previous two.
Invalidate(Region rgn) - Adds the specified graphics region to the update region of the control
            and causes a paint message to be sent to the control.
Invalidate(Region rgn, bool invalidateChildren)

Control.Invalidate(), Form1.Invalidate(), this.Invalidate(), Me.Invalidate()
```
