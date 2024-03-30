
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern IntPtr WindowFromPoint(System.Drawing.Point p);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Private Shared Function WindowFromPoint(ByVal p As Point) As IntPtr
End Function
```

## Oxygene.NET Signature:
```cs
[DllImport("user32.dll")]
class method WindowFromPoint(aPoint: System.Drawing.Point): IntPtr; external;
```

## Sample Code:
```cs
[DllImport("user32.dll")]
static extern bool GetCursorPos(out Point lpPoint);

[DllImport("user32.dll")]
static extern bool SetWindowText(IntPtr hWnd, string lpString);

Point p;
if (GetCursorPos(out p))
{
   IntPtr hWnd = WindowFromPoint(p);
   if (hWnd != IntPtr.Zero) SetWindowText(hWnd, "Window Found");
}
```
