
## C# Signature:
```cs
[DllImport("user32")]
static extern bool AnimateWindow(IntPtr hwnd, int time, AnimateWindowFlags flags);
```

## VB Signature:
```cs
Imports System.Runtime.InteropServices

<DllImport("user32.dll")> _
Shared Function AnimateWindow(ByVal hwnd As IntPtr, ByVal time As Integer, ByVal flags As AnimateWindowFlags) As Boolean
End Function
```

## Tips & Tricks:
```cs
Dim f2 As New Form2
AnimateWindow(f2.Handle, 1000, AnimateWindowFlags.AW_VER_NEGATIVE Or AnimateWindowFlags.AW_SLIDE or AnimateWindowFlags.AW_HIDE)
f2.Show()
```

## C# Sample Code:
```cs
Form2 f2 = new Form2();
AnimateWindow(f2.Handle, 1000, (uint) AnimateWindowFlags.AW_VER_NEGATIVE | (uint) AnimateWindowFlags.AW_SLIDE);
f2.Show();
```

## VB.NET Sample Code:
```cs
Dim f2 As New Form2
AnimateWindow(f2.Handle, 1000, AnimateWindowFlags.AW_VER_NEGATIVE Or AnimateWindowFlags.AW_SLIDE or AnimateWindowFlags.AW_HIDE)
f2.Show()
```
