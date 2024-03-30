
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool ReleaseDC(IntPtr hWnd, IntPtr hDC);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Private Shared Function ReleaseDC(ByVal hWnd As IntPtr, ByVal hDC As IntPtr) As <MarshalAs(UnmanagedType.Bool)> Boolean
End Function
```

## VB Signature:
```cs
Public Declare Function ReleaseDC Lib "user32.dll" _
         (ByVal hWnd As Long, _
          ByVal prmlngHDc As Long) As Long
```
