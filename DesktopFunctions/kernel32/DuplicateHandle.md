
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool DuplicateHandle(IntPtr hSourceProcessHandle,
   IntPtr hSourceHandle, IntPtr hTargetProcessHandle, out IntPtr lpTargetHandle,
   uint dwDesiredAccess, [MarshalAs(UnmanagedType.Bool)] bool bInheritHandle, uint dwOptions);
```

## User-Defined Types:
```cs
[Flags]
  public enum DuplicateOptions : uint
  {
    DUPLICATE_CLOSE_SOURCE = (0x00000001),// Closes the source handle. This occurs regardless of any error status returned.
    DUPLICATE_SAME_ACCESS = (0x00000002), //Ignores the dwDesiredAccess parameter. The duplicate handle has the same access as the source handle.
  }
```
