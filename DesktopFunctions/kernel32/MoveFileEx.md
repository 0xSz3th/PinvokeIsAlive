
## C# Signature:
```cs
[return: MarshalAs(UnmanagedType.Bool)]
[DllImport("kernel32.dll", SetLastError=true, CharSet=CharSet.Unicode)]
static extern bool MoveFileEx(string lpExistingFileName, string lpNewFileName,
   MoveFileFlags dwFlags);
```

## VB.Net Signature:
```cs
Declare Unicode Function MoveFileEx Lib "kernel32.dll" Alias "MoveFileExW" (ByVal lpExistingFileName As String, ByVal lpNewFileName As String, ByVal dwFlags As MoveFileFlags) As Integer
```

## Sample Code:
```cs
// Schedule to next restart dstFile delete and rename of srcFile to dstFile.
MoveFileEx(dstFile, null, MoveFileFlags.MOVEFILE_DELAY_UNTIL_REBOOT);
MoveFileEx(srcFile, dstFile, MoveFileFlags.MOVEFILE_DELAY_UNTIL_REBOOT);
```
