
## C# Signature:
```cs
[DllImport("user32.dll")]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool IsWindowEnabled(IntPtr hWnd);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Private Shared Function IsWindowEnabled(ByVal hWnd As IntPtr) As <MarshalAs(UnmanagedType.Bool)> Boolean
End Function
```
