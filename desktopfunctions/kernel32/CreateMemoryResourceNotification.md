
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
internal static extern IntPtr CreateMemoryResourceNotification(MemoryResourceNotificationType notificationType);
```

## User-Defined Types:
```cs
enum MemoryResourceNotificationType : int
{
    LowMemoryResourceNotification = 0,
    HighMemoryResourceNotification = 1,
}
```
