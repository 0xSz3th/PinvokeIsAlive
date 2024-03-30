
## C# Signature:
```cs
[DllImport("wtsapi32.dll", SetLastError=true)]
static extern IntPtr WTSOpenServer(string pServerName);
```

## VB Signature:
```cs
<DllImport("wtsapi32.dll", CharSet:=CharSet.Auto, SetLastError:=True)> _
Private Shared Function WTSOpenServer(ByVal pServerName As String) As IntPtr
End Function
```
