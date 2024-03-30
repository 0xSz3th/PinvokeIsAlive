
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError=true, CharSet=CharSet.Auto)]
static extern bool SendMessageCallback(IntPtr hWnd, uint Msg, UIntPtr wParam,
    IntPtr lParam, SendMessageDelegate lpCallBack, UIntPtr dwData);
```
