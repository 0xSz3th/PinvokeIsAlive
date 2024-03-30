
## C# Signature:
```cs
[DllImport("kernel32.dll", CharSet=CharSet.Auto)]
static extern bool FindNextFile(IntPtr hFindFile, out WIN32_FIND_DATA
   lpFindFileData);
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll", CharSet:=CharSet.Auto)> _
    Private Function FindNextFile(ByVal hFindFile As IntPtr, ByRef lpFindFileData As WIN32_FIND_DATA) As Boolean
End Function
```

## VB.NET Signature:
```cs
Public Declare Function FindNextFile Lib "kernel32" Alias "FindNextFileA" (ByVal hFindFile As IntPtr, ByRef lpFindFileData As WIN32_FIND_DATA) As Boolean
```
