
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool TranslateMessage([In] ref MSG lpMsg);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Public Shared Function TranslateMessage( _
     ByRef lpMsg As MSG) As <MarshalAs(UnmanagedType.Bool)> Boolean
End Function
```

## VB Signature
```cs
Public Declare Function TranslateMessage Lib "user32" _
         (byref lpMsg As MSG) As Long
```

## Sample Code:
```cs
public struct MSG
     {
     public IntPtr hwnd;
     public uint message;
     public IntPtr wParam;
     public IntPtr lParam;
     public uint time;
     public POINT pt;
     }

     [StructLayout(LayoutKind.Sequential)]
     public struct POINT
     {
     public int X;
     public int Y;

     public POINT(int x, int y)
     {
         this.X = x;
         this.Y = y;
     }

     public static implicit operator System.Drawing.Point(POINT p)
     {
         return new System.Drawing.Point(p.X, p.Y);
     }

     public static implicit operator POINT(System.Drawing.Point p)
     {
         return new POINT(p.X, p.Y);
     }
     }
```

## Sample Code:
```cs
MSG myMsg = new MSG();
        while (WindowsAPIs.GetMessage(out msg, IntPtr.Zero, 0, 0) && ! FOO_EXPRESSION )
        {
        if(msg.message != FILTERED_MESSAGE)
        {
            WindowsAPIs.TranslateMessage(ref msg);
            WindowsAPIs.DispatchMessage(ref msg);
        }
        }
```
