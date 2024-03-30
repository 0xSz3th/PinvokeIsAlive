
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern int GetWindowRgn(IntPtr hWnd, IntPtr hRgn);

//Region Flags - The return value specifies the type of the region that the function obtains. It can be one of the following values.
const int ERROR           = 0;
const int NULLREGION      = 1;
const int SIMPLEREGION    = 2;
const int COMPLEXREGION   = 3;
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Private Shared Function GetWindowRgn(ByVal hWnd As IntPtr, ByVal hRgn As IntPtr) As Integer
End Function
```
