
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError = true)]
static extern bool UnhookWindowsHookEx(IntPtr hhk);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", SetLastError := True)> _
Public Shared Function UnhookWindowsHookEx(ByVal hhk As IntPtr) As Boolean
End Function
```
