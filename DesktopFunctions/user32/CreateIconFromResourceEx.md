
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern IntPtr CreateIconFromResourceEx(byte [] pbIconBits, uint
   cbIconBits, bool fIcon, uint dwVersion, int cxDesired, int cyDesired,
   uint uFlags);
```

## VB Signature:
```cs
<DllImport("user32.dll", SetLastError:=True)> _
    Public Shared Function CreateIconFromResourceEx(ByVal pbIconBits As Byte(), _
                            ByVal cbIconBits As Integer, _
                            ByVal fIcon As Boolean, _
                            ByVal dwVersion As Integer, _
                            ByVal cxDesired As Integer, _
                            ByVal cyDesired As Integer, _
                            ByVal flags As Integer) As IntPtr
    End Function
```
