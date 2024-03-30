
## User-Defined Types C#:
```cs
[StructLayout(LayoutKind.Sequential)]
  public struct NativeMessage 
  {
      public IntPtr handle;
      public uint msg;
      public IntPtr wParam;
      public IntPtr lParam;
      public uint time;
      public System.Drawing.Point p;
  }
```

## User-Defined Types VB.NET:
```cs
Public Structure NativeMessage
    Public handle As IntPtr
    Public msg As UInteger
    Public wParam As IntPtr
    Public lParam As IntPtr
    Public time As UInteger
    Public p As System.Drawing.Point
    End Structure
```

## C# Signature:
```cs
[DllImport("user32.dll")]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool PeekMessage(out NativeMessage lpMsg, HandleRef hWnd, uint wMsgFilterMin,
   uint wMsgFilterMax, uint wRemoveMsg);
```

## VB.NET Signature:
```cs
ByVal filterMin As UInteger, ByVal filterMax As UInteger, ByVal flags As UInteger) _
    As <MarshalAs(UnmanagedType.Bool)> Boolean
    End Function
```

## Tips & Tricks 2:
```cs
NativeMessage msg = new NativeMessage();
GCHandle handle = GCHandle.Alloc(msg);
bool foundMessage = PeekMessage(ref msg, hWnd, 0, 0, 0);
handle.Free();
```

## Sample Code:
```cs
NativeMessage message = new NativeMessage();
PeekMessage(
    out message, 
    new HandleRef(myWindow,myWindow.hWnd),
    0,
    0,
    PM_REMOVE);
```

## C# Signature:
```cs
[SuppressUnmanagedCodeSecurity]
  [return: MarshalAs(UnmanagedType.Bool)]
  [DllImport("User32.dll", CharSet = CharSet.Auto, SetLastError = true)]
  public static extern bool PeekMessage(out NativeMessage message, IntPtr handle, uint filterMin, uint filterMax, uint flags);
```

## Sample Code:
```cs
NativeMessage msg;
  bool foundMessage = PeekMessage(out msg, IntPtr.Zero, 0, 0, 0);
```
