
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern IntPtr CreateRemoteThread(IntPtr hProcess,
   IntPtr lpThreadAttributes, uint dwStackSize, ThreadStartDelegate
   lpStartAddress, IntPtr lpParameter, uint dwCreationFlags, IntPtr lpThreadId);

[DllImport("kernel32.dll")]
static extern IntPtr CreateRemoteThread(IntPtr hProcess, 
   IntPtr lpThreadAttributes, uint dwStackSize, IntPtr lpStartAddress,
   IntPtr lpParameter, uint dwCreationFlags, out IntPtr lpThreadId);
```

## Boo Signature:
```cs
[DllImport("kernel32")]
def CreateRemoteThread(hProcess as IntPtr, lpThreadAttributes as IntPtr, dwStackSize as int, lpStartAddress as IntPtr, lpParameter as IntPtr, dwCreationFlags as uint, ref lpThreadId as IntPtr) as IntPtr:
      pass
```
