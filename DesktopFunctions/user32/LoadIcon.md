
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern IntPtr LoadIcon(IntPtr hInstance, string lpIconName);
```

## C# Signature:
```cs
[DllImport("user32.dll")]
static extern IntPtr LoadIcon(IntPtr hInstance, IntPtr lpIconName);
```

## VB Signature:
```cs
<DllImport("user32.dll")> _
Private Shared Function LoadIcon(ByVal hInstance As IntPtr, ByVal lpIconName As String) As IntPtr
End Function

' For loading icon-resource identified as integer ID
<DllImport("user32.dll")> _
Private Shared Function LoadIcon(ByVal hInstance As IntPtr, ByVal lpIconName As IntPtr) As IntPtr
End Function
```
