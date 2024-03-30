
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true)]
static extern bool GetSystemTimes (
            out FILETIME lpIdleTime, 
            out FILETIME lpKernelTime, 
            out FILETIME lpUserTime
            );
```

## Sample Code:
```cs
FILETIME idleTime, kernelTime, userTime;
    GetSystemTimes(out idleTime, out kernelTime, out userTime);
    ulong idleTimeLong = ((ulong)idleTime.dwHighDateTime << 32) + (uint)idleTime.dwLowDateTime; 
    return (int)(idleTimeLong / TimeSpan.TicksPerMillisecond);
```
