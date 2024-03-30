
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool EmptyClipboard();
```

## Sample Code:
```cs
IntPtr handleWnd = GetOpenClipboardWindow();
OpenClipboard(handleWnd);
EmptyClipboard();
CloseClipboard();
```
