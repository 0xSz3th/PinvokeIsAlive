
## C# Signature:
```cs
[DllImport("advapi32.dll", EntryPoint = "QueryServiceStatus", CharSet = CharSet.Auto)]
public static extern bool QueryServiceStatus(IntPtr hService,ref SERVICE_STATUS dwServiceStatus);
```

## VB.NET Signature:
```cs
<Runtime.InteropServices.DllImport("advapi32.dll", CharSet:=Runtime.InteropServices.CharSet.Auto, SetLastError:=True)> _
Public Shared Function QueryServiceStatus(ByVal hService As IntPtr, ByRef dwServiceStatus As SERVICE_STATUS) As Boolean
End Function
```

## VB Signature:
```cs
Declare Function QueryServiceStatus Lib "advapi32.dll" (TODO) As TODO
```
