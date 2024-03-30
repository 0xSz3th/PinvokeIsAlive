
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool GetAltTabInfo(IntPtr hwnd, int iItem, out ALTTABINFO pati,
   [Out] StringBuilder pszItemText, uint cchItemText);
```

## VB.NET Signature:
```cs
Private Shared Function GetAltTabInfo( _
  ByVal hwnd As IntPtr, _
  ByVal iItem As Integer, _
  ByRef pati As ALTTABINFO, _
  ByRef pszItemText As System.Text.StringBuilder, _
  ByVal cchItemText As UInt32) As Boolean
End Function
```
