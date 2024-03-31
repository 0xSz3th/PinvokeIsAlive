
## C# Definition:
```cs
[DllImport("dwmapi.dll", PreserveSig = true)]
public static extern int DwmSetWindowAttribute(IntPtr hwnd, DWMWINDOWATTRIBUTE attr, ref int attrValue, int attrSize);
```

## VB Definition:
```cs
<DllImport("dwmapi.dll", PreserveSig:=True)>
Public Shared Function DwmSetWindowAttribute(hwnd As IntPtr, attr As DWMWINDOWATTRIBUTE, ByRef attrValue As Integer, attrSize As Integer) As Integer
End Function
```
