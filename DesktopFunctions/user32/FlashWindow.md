
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool FlashWindow(IntPtr hwnd, bool bInvert);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Private Shared Function FlashWindow(hwnd As IntPtr, bInvert As Boolean) As Boolean
End Function
```

## Sample Code:
```cs
[DllImport("user32.dll")]
    private static extern bool FlashWindow(IntPtr hwnd, bool bInvert);

    public static void FlashWindow(System.Windows.Forms.Form window)
    {
        FlashWindow(window.Handle, false);
    }
```
