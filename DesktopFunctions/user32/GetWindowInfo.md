
## C# Signature:
```cs
[return: MarshalAs(UnmanagedType.Bool)]
[DllImport("user32.dll",SetLastError = true)]
private static extern bool GetWindowInfo(IntPtr hwnd, ref WINDOWINFO pwi);
```

## VB Signature:
```cs
Public Declare Auto Function GetWindowInfo Lib "user32" _
(ByVal hwnd As IntPtr, ByRef pwi As WINDOWINFO) As Boolean
```

## VB.Net Signature:
```cs
<DllImport("user32.dll",SetLastError:= True)> _
Public Shared Function GetWindowInfo(ByVal hwnd As IntPtr, ByRef pwi As WINDOWINFO) As Boolean
End Function
```

## Notes:
```cs
WINDOWINFO info = new WINDOWINFO();
    info.cbSize = (uint)Marshal.SizeOf(info);
    GetWindowInfo(Handle, ref info);
```

## Notes:
```cs
Dim info As New WINDOWINFO
    info.cbSize = Convert.ToUInt32(Marshal.SizeOf(info))
    GetWindowInfo(Handle, info)
```
