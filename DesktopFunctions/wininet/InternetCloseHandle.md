
## C# Signature:
```cs
[DllImport("wininet.dll", SetLastError=true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool InternetCloseHandle(IntPtr hInternet);
```

## VB Signature:
```cs
Public Declare Function InternetCloseHandle Lib "wininet.dll" ( _
    ByVal hInet As IntPtr) As <MarshalAs(UnmanagedType.Bool)> Boolean
```
