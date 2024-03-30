
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError=true)]
static extern IntPtr GetDC(IntPtr hWnd);
```

## VB Signature:
```cs
<DllImport("user32.dll")> _
Public Shared Function GetDC(ByVal hwnd As IntPtr) As IntPtr
End Function
```

## VB Signature
```cs
Public Declare Function GetDC Lib "user32.dll" _
         (ByVal hWnd As Long) As Long
```
