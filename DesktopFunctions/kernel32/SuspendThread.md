
## C# Signature:
```cs
[DllImport("kernel32.dll",SetLastError=true)]
static extern int SuspendThread(IntPtr hThread);
```

## VB Signature:
```cs
<DllImport("kernel32.dll",SetLastError:=True)> _
Function SuspendThread(hThread As IntPtr ) As Integer
End Function
```

## Boo Signature:
```cs
[DllImport("kernel32.dll")]
def SuspendThread(threadHandle as IntPtr) as int:
     pass
```

## Sample Code:
```cs
{
       Process p = Process.GetProcessById((int)pid);
       foreach (ProcessThread thd in p.Threads)
       {
           IntPtr threadHandle = OpenThread(THREADACCESS_SUSPEND_RESUME, false, (uint)thd.Id); // Open thread with required permissions
           if (threadHandle == IntPtr.Zero) // If thread pointer is zero, means that the 'OpenThread' function has failed
           {
           throw new Win32Exception((int)GetLastError());
           }
           if (SuspendThread(threadHandle) == -1) // If the result is -1, the funtion has failed
           {
           CloseHandle(threadHandle);
           throw new Win32Exception((int)GetLastError());
           }
           CloseHandle(threadHandle); // Don't forget close thread handle
       }
       p.Dispose();
       }
```
