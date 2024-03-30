
## C# Signature:
```cs
[DllImport("kernel32.dll")]
private static extern bool Wow64SetThreadContext(IntPtr thread, int[] context);
```

## VB Signature:
```cs
<DllImport("kernel32.dll", EntryPoint:="Wow64GetThreadContext"), SuppressUnmanagedCodeSecurity> _
    Private Shared Function Wow64GetThreadContext( _
    ByVal thread As IntPtr, _
    ByVal context As Integer()) As Boolean
    End Function
```
