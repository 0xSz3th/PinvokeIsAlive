
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern IntPtr FindFirstChangeNotification(string lpPathName,
   bool bWatchSubtree, uint dwNotifyFilter);
```

## Alternative Managed API:
```cs
System.IO.FileSystemWatcher
```
