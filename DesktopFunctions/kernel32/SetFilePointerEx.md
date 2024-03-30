
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool SetFilePointerEx(IntPtr hFile, long liDistanceToMove,
   IntPtr lpNewFilePointer, uint dwMoveMethod);
```

## C# Signature:
```cs
[DllImport("kernel32.dll")]
public static extern bool SetFilePointerEx(
     SafeFileHandle hFile, long liDistanceToMove,
     out long lpNewFilePointer, uint dwMoveMethod);
```
