
## C# Signature:
```cs
[DllImport("user32.dll", EntryPoint="GetWindowLong")]
static extern IntPtr GetWindowLongPtr(IntPtr hWnd, int nIndex);
```

## VB .NET Signature:
```cs
<DllImport("user32.dll", EntryPoint:="GetWindowLong")> _
Private Shared Function GetWindowLongPtr(ByVal hWnd As HandleRef, <MarshalAs(UnmanagedType.I4)>nIndex As WindowLongFlags) As IntPtr
End Function
```

## VB Signature:
```cs
Public Declare Function GetWindowLong Lib "user32.dll" Alias "GetWindowLongA" _
        (ByVal prmlngWindowHandle As Long, _
         ByVal prmlngIndex As WindowLongFlags) As Long
```

## C# Signature:
```cs
[DllImport("user32.dll", EntryPoint="GetWindowLongPtr")]
private static extern IntPtr GetWindowLongPtr(IntPtr hWnd, int nIndex);
```

## VB .NET Signature:
```cs
<DllImport("user32.dll", EntryPoint:="GetWindowLongPtr")> _
Private Shared Function GetWindowLongPtr(ByVal hWnd As HandleRef, <MarshalAs(UnmanagedType.I4)>nIndex As WindowLongFlags) As IntPtr
End Function
```

## VB Signature:
```cs
Public Declare Function GetWindowLong Lib "user32.dll" Alias "GetWindowLongA" _
        (ByVal prmlngWindowHandle As Long, _
         ByVal prmlngIndex As WindowLongFlags) As Long
```

## User-Defined Types:
```cs
public enum GWL
{
     GWL_WNDPROC =    (-4),
     GWL_HINSTANCE =  (-6),
     GWL_HWNDPARENT = (-8),
     GWL_STYLE =      (-16),
     GWL_EXSTYLE =    (-20),
     GWL_USERDATA =   (-21),
     GWL_ID =     (-12)
}
```

## User-Defined Types:
```cs
Public Enum GWL
     GWL_WNDPROC = -4
     GWL_HINSTANCE = -6
     GWL_HWNDPARENT = -8
     GWL_STYLE = -16
     GWL_EXSTYLE = -20
     GWL_USERDATA = -21
     GWL_ID = -12
End Enum
```

## Tips & Tricks:
```cs
[DllImport("user32.dll", EntryPoint="GetWindowLong")]
private static extern IntPtr GetWindowLongPtr32(IntPtr hWnd, int nIndex);

[DllImport("user32.dll", EntryPoint="GetWindowLongPtr")]
private static extern IntPtr GetWindowLongPtr64(IntPtr hWnd, int nIndex);

// This static method is required because Win32 does not support
// GetWindowLongPtr directly
public static IntPtr GetWindowLongPtr(IntPtr hWnd, int nIndex)
{
     if (IntPtr.Size == 8)
     return GetWindowLongPtr64(hWnd, nIndex);
     else
     return GetWindowLongPtr32(hWnd, nIndex);
}
```

## Tips & Tricks:
```cs
<DllImport("user32.dll", EntryPoint:="GetWindowLong")> _
Private Shared Function GetWindowLongPtr32(ByVal hWnd As HandleRef, ByVal nIndex As Integer) As IntPtr
End Function

<DllImport("user32.dll", EntryPoint:="GetWindowLongPtr")> _
Private Shared Function GetWindowLongPtr64(ByVal hWnd As HandleRef, ByVal nIndex As Integer) As IntPtr
End Function

' This static method is required because Win32 does not support GetWindowLongPtr dirctly
Public Shared Function GetWindowLongPtr(ByVal hWnd As HandleRef, ByVal nIndex As Integer) As IntPtr
     If IntPtr.Size = 8 Then
      Return GetWindowLongPtr64(hWnd, nIndex)
     Else
      Return GetWindowLongPtr32(hWnd, nIndex)
     End If
End Function
```

## Sample Code:
```cs
//Returns the ID for a window given the handle for that window as returned by EnumChildWindows.
//note that for this to work you will need to change the signature from 'int nIndex' to 'GWL nIndex' in all three places
private string GetID(IntPtr winhandle)
{
     IntPtr result;
     result = GetWindowLongPtr(winhandle, GWL.GWL_ID);
     return result.ToString();
}
```
