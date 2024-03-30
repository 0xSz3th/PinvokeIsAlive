
## C# Signature:
```cs
[DllImport("shell32.dll", CharSet=CharSet.Unicode)]
static extern UInt32 SHSetUnreadMailCount(string pszMailAddress, UInt32 dwCount, string pszShellExecuteCommand);
```

## VB Signature:
```cs
<DllImport("shell32.dll", CharSet:=CharSet.Unicode)> _
  Public Shared Function SHSetUnreadMailCount(ByVal pszMailAddress As String, ByVal dwCount As Integer, ByVal pszShellExecuteCommand As String) As Integer
```
