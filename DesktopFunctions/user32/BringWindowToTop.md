
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError=true)]
static extern bool BringWindowToTop(IntPtr hWnd);

[DllImport("user32.dll", SetLastError=true)]
static extern bool BringWindowToTop(HandleRef hWnd);
```

## VB Signature:
```cs
<DllImport("user32.dll", SetLastError:=True)> _
Private Shared Function BringWindowToTop(ByVal hwnd As IntPtr) As Boolean
End Function
'Or just
Public Declare Function BringWindowToTop Lib "user32" (ByVal HWnd As IntPtr) As Boolean
```
