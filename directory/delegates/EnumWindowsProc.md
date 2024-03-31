
## C# Definition:
```cs
private delegate bool EnumWindowsProc(IntPtr hWnd, IntPtr lParam);
```

## VB Definition:
```cs
Private Delegate Function EnumWindowsProc(ByVal hWnd As IntPtr, ByVal lParam As IntPtr) As Boolean
```

## Notes:
```cs
private delegate bool EnumWindowsProc(IntPtr hWnd, ref IntPtr lParam);
```

## Notes:
```cs
Private Delegate Function EnumWindowsProc(ByVal hWnd As IntPtr, ByRef lParam As IntPtr) As Boolean
```
