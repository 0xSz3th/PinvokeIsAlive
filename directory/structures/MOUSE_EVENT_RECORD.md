
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
  public struct MOUSE_EVENT_RECORD
  {
    public COORD dwMousePosition;
    public MouseButtonState dwButtonState;
    public ControlKeyState dwControlKeyState;
    public MouseEventFlags dwEventFlags;
  }

  [Flags]
  public enum MouseButtonState
  {
    FROM_LEFT_1ST_BUTTON_PRESSED = 0x1,
    RIGHTMOST_BUTTON_PRESSED = 0x2,
    FROM_LEFT_2ND_BUTTON_PRESSED = 0x4,
    FROM_LEFT_3RD_BUTTON_PRESSED = 0x8,
    FROM_LEFT_4TH_BUTTON_PRESSED = 0x10
  }

  [Flags]
  public enum ControlKeyState 
  {
    RIGHT_ALT_PRESSED = 0x1,
    LEFT_ALT_PRESSED = 0x2,
    RIGHT_CTRL_PRESSED = 0x4,
    LEFT_CTRL_PRESSED = 0x8,
    SHIFT_PRESSED = 0x10,
    NUMLOCK_ON = 0x20,
    SCROLLLOCK_ON = 0x40,
    CAPSLOCK_ON = 0x80,
    ENHANCED_KEY = 0x100
  }

  [Flags]
  public enum MouseEventFlags
  {
    MOUSE_MOVED = 0x1,
    DOUBLE_CLICK = 0x2,
    MOUSE_WHEELED = 0x4,
    MOUSE_HWHEELED = 0x8
  }
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Explicit)> _
    Public Structure MOUSE_EVENT_RECORD
        <FieldOffset(0)>
        Public dwMousePosition As COORD
        <FieldOffset(4)>
        Public dwButtonState As UInteger
        <FieldOffset(8)>
        Public dwControlKeyState As UInteger
        <FieldOffset(12)>
        Public dwEventFlags As UInteger
    End Structure
```
