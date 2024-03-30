
## C# Signature:
```cs
[DllImport("ntdll.dll")]
public static extern int NtQueryDirectoryObject(
   SafeFileHandle DirectoryHandle,
   IntPtr Buffer,
   int Length,
   bool ReturnSingleEntry,
   bool RestartScan,
   ref uint Context,
   out uint ReturnLength);
```
