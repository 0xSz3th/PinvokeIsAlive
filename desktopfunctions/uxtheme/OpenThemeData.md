
## C# Signature:
```cs
[DllImport("uxtheme.dll", ExactSpelling=true, CharSet=CharSet.Unicode)]
public static extern IntPtr OpenThemeData(IntPtr hWnd, String classList);
```

## VB .NET Signature:
```cs
Declare Function OpenThemeData Lib "uxtheme.dll" (hWnd As IntPtr, classList As String) As IntPtr

<DllImport("UxTheme.dll", CallingConvention:=CallingConvention.Cdecl, CharSet:=CharSet.Unicode)> _
Function OpenThemeData( ByVal hwnd As IntPtr, ByVal pszClassList As String) As IntPtr
End Function
```
