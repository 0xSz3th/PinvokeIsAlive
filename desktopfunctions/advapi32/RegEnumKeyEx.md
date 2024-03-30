
## C# Signature:
```cs
[DllImport("advapi32.dll", EntryPoint = "RegEnumKeyEx")]
extern private static int RegEnumKeyEx(UIntPtr hkey,
    uint index,
    StringBuilder lpName,
    ref uint lpcbName,
    IntPtr reserved,
    IntPtr lpClass,
    IntPtr lpcbClass,
    out long lpftLastWriteTime);
```

## VB Signature:
```cs
Declare Auto Function RegEnumKeyEx Lib "Advapi32" ( _
   ByVal hKey As IntPtr, _
   ByVal dwIndex As Integer, _
   ByVal lpName As StringBuilder, _
   ByRef lpcName As Integer, _
   ByVal lpReserved As IntPtr, _
   ByVal lpClass As IntPtr, _
   ByVal lpcClass As IntPtr, _
   ByVal lpftLastWriteTime As IntPtr _
) As Integer
```

## Notes:
```cs
LONG RegEnumKeyEx(
   HKEY hKey,
   DWORD dwIndex,
   LPTSTR lpName,
   LPDWORD lpcName,
   LPDWORD lpReserved,
   LPTSTR lpClass,
   LPDWORD lpcClass,
   PFILETIME lpftLastWriteTime
);
```

## Sample Code:
```cs
Public Function GetSubKeyNames() As String()
   Dim i, ret, NameSize As Integer
   Dim sc As New StringCollection
   Dim sb As New StringBuilder(MAX_REG_KEYNAME_SIZE + 1)
   Dim ans(-1) As String

   ' quick sanity check
   If hKey.Equals(IntPtr.Zero) Then
     Throw New ApplicationException("Cannot access a closed registry key")
   End If

   Do
     NameSize = MAX_REG_KEYNAME_SIZE + 1
     ret = RegEnumKeyEx(hKey, i, sb, NameSize, IntPtr.Zero, IntPtr.Zero, IntPtr.Zero, IntPtr.Zero)
     If ret <> 0 Then
       Exit Do
     End If
     sc.Add(sb.ToString)
     i += 1
   Loop

   If sc.Count > 0 Then
     ReDim ans(sc.Count - 1)
     sc.CopyTo(ans, 0)
   End If
   Return ans
End Function
```
