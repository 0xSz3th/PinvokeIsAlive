
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern IntPtr GetDCEx(IntPtr hWnd, IntPtr hrgnClip, DeviceContextValues flags);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Private Shared Function GetDCEx(ByVal hWnd As IntPtr, ByVal hrgnClip As IntPtr, ByVal DeviceContextValues As DeviceContextValues) As IntPtr
End Function
```

## VB Signature:
```cs
Private Declare Function Lib "user32.dll" GetDCEx(ByVal hWnd As IntPtr, ByVal hrgnClip As IntPtr, ByVal DeviceContextValues As DeviceContextValues) As IntPtr
```

## Notes:
```cs
<param name="hWnd">
```

## Notes:
```cs
<param name="hrgnClip">
```

## Notes:
```cs
<param name="flags">
```
