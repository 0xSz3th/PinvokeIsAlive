
## C# Signature:
```cs
[DllImport( "kernel32.dll", EntryPoint = "WaitForDebugEvent" )]
[return : MarshalAs( UnmanagedType.Bool )]
public static extern bool WaitForDebugEvent(ref DEBUG_EVENT lpDebugEvent, uint dwMilliseconds );
```
