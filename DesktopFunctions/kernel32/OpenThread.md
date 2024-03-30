
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
static extern Microsoft.Win32.SafeHandles.SafeAccessTokenHandle OpenThread(
   ThreadAccess dwDesiredAccess,
   bool bInheritHandle,
   uint dwThreadId
   );

[DllImport("kernel32.dll", SetLastError = true)]
static extern IntPtr OpenThread(ThreadAccess dwDesiredAccess, bool bInheritHandle,
   uint dwThreadId);
```

## Boo Signature:
```cs
[DllImport("kernel32.dll")]
def OpenThread(dwDesiredAccess as int, bInheritHandle as bool, dwThreadId as int) as IntPtr:
     pass
```

## User-Defined Types:
```cs
[Flags]
  public enum    ThreadAccess : int 
  {
    TERMINATE           = (0x0001)  ,
    SUSPEND_RESUME      = (0x0002)  ,
    GET_CONTEXT         = (0x0008)  ,
    SET_CONTEXT         = (0x0010)  ,
    SET_INFORMATION     = (0x0020)  ,
    QUERY_INFORMATION       = (0x0040)  ,
    SET_THREAD_TOKEN    = (0x0080)  ,
    IMPERSONATE         = (0x0100)  ,
    DIRECT_IMPERSONATION    = (0x0200)
  }
```

## Sample Code:
```cs
private static void SuspendProcess(int pid)
  {
    var process = Process.GetProcessById(pid);
    if (process.ProcessName == string.Empty)
    {
      return;
    }
    foreach (ProcessThread thread in process.Threads)
    {
      using (var handle = 
           OpenThread(
         ThreadAccess.SUSPEND_RESUME,
         false,
         (uint)thread.IdThreadAccess)
        ) // using block ensures finalizer closes handle
      {
        if (!handle.IsInvalid)
        {
          SuspendThread(pOpenThread);
        }
      }
    }
  }
```
