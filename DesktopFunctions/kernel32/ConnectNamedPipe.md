
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool ConnectNamedPipe(IntPtr hNamedPipe,
   [In] ref System.Threading.NativeOverlapped lpOverlapped);
```

##  Alternate C# Signature
```cs
[DllImport("kernel32.dll")]
static extern bool ConnectNamedPipe(IntPtr hNamedPipe, IntPtr lpOverlapped);
```
