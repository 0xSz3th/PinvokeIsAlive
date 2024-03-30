
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern IntPtr BeginDeferWindowPos(int nNumWindows);
```

## VB.NET Signature
```cs
<DllImport("user32.dll", SetLastError:=True)> _
Public Shared Function BeginDeferWindowPos(nNumWindows As Integer) As IntPtr
End Function
```

## VB Signature
```cs
Public Declare Function BeginDeferWindowPos Lib "user32" _
         (ByVal nNumWindows As Long) As Long
```
