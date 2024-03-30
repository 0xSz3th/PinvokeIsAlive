
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool AdjustWindowRect(ref RECT lpRect, uint dwStyle, bool bMenu);
```

## VB.Net Signature:
```cs
<DllImport("user32.dll")> _
Public Function AdjustWindowRect(<MarshalAs(UnmanagedType.Struct)>ByRef lpRect As RECT, _
                  <MarshalAs(UnmanagedType.U4)>dwStyle As WindowStyles, _
                  <MarshalAs(UnmanagedType.Bool)>bMenu As Boolean) As <MarshalAs(UnmanagedType.Bool)> Boolean
End Function
```

## VB Signature:
```cs
Public Declare Function AdjustWindowRect Lib "user32" _
         (lpRect As RECT, _
          ByVal dsStyle As WindowStyles, _
          ByVal bMenu As Long) As Long
```
