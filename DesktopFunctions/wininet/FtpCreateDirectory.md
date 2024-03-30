
## C# Signature:
```cs
[DllImport("wininet.dll", SetLastError=true, CharSet=CharSet.Auto)]
static extern bool FtpCreateDirectory(IntPtr hConnect, string lpszDirectory);
```

## VB Signature:
```cs
<DllImport("wininet.dll", SetLastError := True, CharSet := CharSet.Auto)> _
  Private Shared Function FtpCreateDirectory(ByVal hConnect As IntPtr, ByVal lpszDirectory As String) As Boolean
  End Function
```
