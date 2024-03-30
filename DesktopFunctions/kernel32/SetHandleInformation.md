
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
static extern bool SetHandleInformation(IntPtr hObject, HANDLE_FLAGS dwMask,
   HANDLE_FLAGS dwFlags);
```

## User-Defined Types:
```cs
[Flags]
enum HANDLE_FLAGS: uint
{
     None = 0,
     INHERIT = 1,
     PROTECT_FROM_CLOSE = 2
}
```
