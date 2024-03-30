
## C# Signature:
```cs
[DllImport("user32.dll")]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool SetCursorPos(int x, int y);
```

## VB.Net Signature:
```cs
<DllImport("user32.dll", SetLastError:=True)> _
Private Shared Function SetCursorPos(ByVal X As Integer, ByVal Y As Integer) As Boolean
End Function
```

## Sample Code:
```cs
[DllImport("user32.dll")]
    static extern bool ClientToScreen(IntPtr hwnd, ref Point lpPoint);

    [DllImport("user32.dll")]
    static extern bool SetCursorPos(int X, int Y);

    public void UnmanagedMoveCursorOverButton(Button button)
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

    public void ManagedMoveCursorOverButton(Button button)
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
          point.X += x;
          point.Y += y;
          System.Windows.Forms.Cursor.Position = point;
        }
        }
    }
```

## Alternative Managed API:
```cs
System.Windows.Forms.Cursor.Position
```
