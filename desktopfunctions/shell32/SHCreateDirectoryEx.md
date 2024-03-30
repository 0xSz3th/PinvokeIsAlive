
## C# Signature:
```cs
[DllImport("shell32.dll")]
static extern int SHCreateDirectoryEx(IntPtr hwnd, string pszPath, IntPtr psa);
```

## C# Sample Code:
```cs
SHCreateDirectoryEx(IntPtr.Zero, @"D:\test\", IntPtr.Zero);
```
