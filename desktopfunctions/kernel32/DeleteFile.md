
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool DeleteFile(string lpFileName);

[DllImport("kernel32.dll", SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool DeleteFileA([MarshalAs(UnmanagedType.LPStr)]string lpFileName);

[DllImport("kernel32.dll", SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool DeleteFileW([MarshalAs(UnmanagedType.LPWStr)]string lpFileName);
```

## Sample Code:
```cs
String filePath = @"C:\Data\MyFile.txt";

bool deleted = DeleteFileW(filePath);
if (!deleted)
{
     int lastError = Marshal.GetLastWin32Error();
     Console.WriteLine("Failed to delete '{1}': error={0}", lastError, filePath);
}
```
