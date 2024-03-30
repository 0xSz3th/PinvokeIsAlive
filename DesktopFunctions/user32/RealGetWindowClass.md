
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern uint RealGetWindowClass(IntPtr hwnd, [Out] StringBuilder pszType,
   uint cchType);
```

## VB Signature:
```cs
<DllImport("user32.dll", SetLastError:=True)> _
Private Shared Function RealGetWindowClass(ByVal hWnd As IntPtr, _
                        ByVal lpString As StringBuilder, _
                        ByVal nMaxCount As Integer) As Integer
End Function
```

## Sample Code:
```cs
public static string RealGetWindowClassM(IntPtr hWnd)
{
    StringBuilder pszType = new StringBuilder();
    pszType.Capacity = 255;
    RealGetWindowClass(hWnd, pszType, (UInt32)pszType.Capacity);
    return pszType.ToString();
}
```
