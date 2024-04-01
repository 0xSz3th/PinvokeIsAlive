# MSG

\[StructLayout(LayoutKind.Sequential)]

public struct MSG {     IntPtr hwnd;     uint message;     UIntPtr wParam;     IntPtr lParam;     int time;     POINT pt;     int lPrivate; }

### VB Definition:

```cs
TODO
```

### User-Defined Field Types:

```cs
// Delegate declaration for a callback that gets called when the help button on the message box is pushed.
public delegate void MsgBoxCallback( [HELPINFO] lpHelpInfo );
```

### Notes:

```cs
None.
```
