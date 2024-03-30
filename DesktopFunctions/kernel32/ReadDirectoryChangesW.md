
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool ReadDirectoryChangesW(IntPtr hDirectory, IntPtr lpBuffer,
   uint nBufferLength, bool bWatchSubtree, uint dwNotifyFilter, out uint
   lpBytesReturned, IntPtr lpOverlapped,
   ReadDirectoryChangesDelegate lpCompletionRoutine);
```

## Alternative Managed API:
```cs
System.IO.FileSystemWatcher
```
