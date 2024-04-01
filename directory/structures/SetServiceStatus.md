# SetServiceStatus

myServiceStatus.currentState = (int)State.SERVICE\_START\_PENDING;         myServiceStatus.checkPoint = 1;         myServiceStatus.waitHint = 5000;         SetServiceStatus(handle, ref myServiceStatus) myServiceStatus.currentState = (int)State.SERVICE\_RUNNING;         myServiceStatus.checkPoint = 0;         myServiceStatus.waitHint = 0;         SetServiceStatus(handle, ref myServiceStatus);

### C# Definition:

```cs
[DllImport("advapi32.dll")]
   private static extern bool SetServiceStatus(IntPtr hServiceStatus, ref SERVICE_STATUS lpServiceStatus);
```

### VB Definition:

```cs
ByVal hServiceStatus As IntPtr, 
    ByRef lpServiceStatus As SERVICE_STATUS) 
    As Integer
```

### User-Defined Field Types:

```cs
public enum State
    {
    SERVICE_STOPPED = 0x00000001,
    SERVICE_START_PENDING = 0x00000002,
    SERVICE_STOP_PENDING = 0x00000003,
    SERVICE_RUNNING = 0x00000004,
    SERVICE_CONTINUE_PENDING = 0x00000005,
    SERVICE_PAUSE_PENDING = 0x00000006,
    SERVICE_PAUSED = 0x00000007,
    }

   [StructLayout(LayoutKind.Sequential)]
   public struct SERVICE_STATUS {
       public long serviceType;
       public State currentState;
       public long controlsAccepted;
       public long win32ExitCode;
       public long serviceSpecificExitCode;
       public long checkPoint;
       public long waitHint;
   };
```
