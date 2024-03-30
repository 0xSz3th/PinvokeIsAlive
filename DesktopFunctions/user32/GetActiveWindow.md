
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern IntPtr GetActiveWindow();
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", SetLastError:=True)> _
Private Shared Function GetActiveWindow() As IntPtr
End Function
```

## VB Signature:
```cs
Public Declare Function GetActiveWindow Lib "user32.dll" () As Long
```

## Sample Code:
```cs
if (GetActiveWindow() == Handle) {
    // The Form is the active window
}
```
