
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError=true)]
static extern Int32 RegUnLoadKey(
    UInt32 hKey,
    string lpSubKey);
```

## VB Signature:
```cs
Private Declare Auto Function RegUnLoadKey Lib "advapi32.dll" ( _
   ByVal hKey As IntPtr, _
   ByVal lpSubKey As String _
) As Integer
```

## Notes:
```cs
LONG RegUnLoadKey(
   HKEY hKey,
   LPCTSTR lpSubKey
);
```

## Sample Code:
```cs
Public Shared Sub UnLoadKey(ByVal Key As RegistryKey, ByVal MountPoint As String)
   Dim ret As Integer
   ret = RegUnLoadKey(Key.hKey, MountPoint)
   If ret <> 0 Then
     Throw New Win32Exception(ret)
   End If
End Sub
```
