
## C# Signature:
```cs
// This helper static method is required because the 32-bit version of user32.dll does not contain this API
// (on any versions of Windows), so linking the method will fail at run-time. The bridge dispatches the request
// to the correct function (GetWindowLong in 32-bit mode and GetWindowLongPtr in 64-bit mode)
public static IntPtr SetWindowLongPtr(HandleRef hWnd, int nIndex, IntPtr dwNewLong)
{
      if (IntPtr.Size == 8)
      return SetWindowLongPtr64(hWnd, nIndex, dwNewLong);
      else
      return new IntPtr(SetWindowLong32(hWnd, nIndex, dwNewLong.ToInt32()));
}

[DllImport("user32.dll", EntryPoint="SetWindowLong")]
private static extern int SetWindowLong32(HandleRef hWnd, int nIndex, int dwNewLong);

[DllImport("user32.dll", EntryPoint="SetWindowLongPtr")]
private static extern IntPtr SetWindowLongPtr64(HandleRef hWnd, int nIndex, IntPtr dwNewLong);
//
If that doesn't work, the following signature can be used alternatively.
//
[DllImport("user32.dll")]
static extern int SetWindowLong(IntPtr hWnd, int nIndex, uint dwNewLong);
```

## VB.NET Signature:
```cs
<System.Runtime.InteropServices.DllImport("user32.dll", EntryPoint:="SetWindowLong")> _
  Private Shared Function SetWindowLong32(ByVal hWnd As IntPtr, <MarshalAs(UnmanagedType.I4)>nIndex As WindowLongFlags, ByVal dwNewLong As Integer) As Integer
  End Function

  <System.Runtime.InteropServices.DllImport("user32.dll", EntryPoint:="SetWindowLongPtr")> _
  Private Shared Function SetWindowLongPtr64(ByVal hWnd As IntPtr, <MarshalAs(UnmanagedType.I4)>nIndex As WindowLongFlags, ByVal dwNewLong As IntPtr) As IntPtr
  End Function

  Public Shared Function SetWindowLongPtr(ByVal hWnd As IntPtr, nIndex As WindowLongFlags, ByVal dwNewLong As IntPtr) As IntPtr
    If IntPtr.Size = 8 Then
      Return SetWindowLongPtr64(hWnd, nIndex, dwNewLong)
    Else
      Return New IntPtr(SetWindowLong32(hWnd, nIndex, dwNewLong.ToInt32))
    End If
  End Function
```

## VB.NET Signature:
```cs
Public Declare Function SetWindowLongPtr Lib "user32" Alias "SetWindowLongPtrA" _
        (ByVal hWnd As Long, _
         ByVal nIndex As WindowLongFlags, _
         ByVal dwNewLong As Long) As Long
```

## Tips & Tricks:
```cs
GWL_EXSTYLE needs a value of -0x14.
    WS_EX_NOACTIVATE needs a value of 0x08000000.
    WS_EX_APPWINDOW needs a value of 0x40000.
```

## Tips & Tricks:
```cs
SetWindowLong(GetPinvokeHandle(), GWL_EXSTYLE, WS_EX_APPWINDOW);
```

## Tips & Tricks:
```cs
SetWindowLong(GetPinvokeHandle(), GWL_EXSTYLE, WS_EX_NOACTIVATE);
```
