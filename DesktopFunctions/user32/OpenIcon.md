
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool OpenIcon(IntPtr hWnd);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", SetLastError:=True)> _
Public Function OpenIcon(hWnd As IntPtr) As <MarshalAs(UnmanagedType.Bool)> Boolean

End Function
```

## VB Signature:
```cs
Public Declare Function OpenIcon Lib "user32" _
         (ByVal hWnd As Long) As Long
```
