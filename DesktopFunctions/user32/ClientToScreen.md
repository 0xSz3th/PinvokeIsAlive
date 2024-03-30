
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool ClientToScreen(IntPtr hWnd, ref POINT lpPoint);
```

## VB Signature:
```cs
<DllImport("user32.dll")> _
Private Shared Function ClientToScreen(ByVal hWnd As IntPtr, ByRef lpPoint As POINT) As Boolean
End Function
```

## Sample Code:
```cs
[DllImport("user32.dll")]
    static extern bool ClientToScreen(IntPtr hwnd, ref Point lpPoint);

    [DllImport("user32.dll")]
    static extern bool SetCursorPos(int X, int Y);

    public void MoveCursorOverButton(Button button)
    {
        IntPtr handle = IntPtr.Zero;
        Point point;
        int x = 0;
        int y = 0;
        int width = 0;
        int height = 0;
        bool coordinatesFound = false;
```

## Sample Code:
```cs
if (button != null)
        {
        width = button.Size.Width;
        height = button.Size.Height;
        handle = button.Handle;
        }

        if ((width > 0) && (height > 0))
        {
        point = new Point();
        x = (width / 2);
        y = (height / 2);

        coordinatesFound = ClientToScreen(handle, ref point);

        if (coordinatesFound == true)
        {
            SetCursorPos(point.X + x, point.Y + y);
        }
        }
    }
```

## Alternative Managed API:
```cs
Control.PointToScreen
Control.RectangleToScreen
```
