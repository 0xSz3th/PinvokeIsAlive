
## C# Signature:
```cs
[DllImport("kernel32.dll", CharSet = CharSet.Auto,SetLastError = true)]
static extern EXECUTION_STATE SetThreadExecutionState(EXECUTION_STATE esFlags);
```

## User-Defined Types:
```cs
[FlagsAttribute]
public enum EXECUTION_STATE :uint
{
     ES_AWAYMODE_REQUIRED = 0x00000040,
     ES_CONTINUOUS = 0x80000000,
     ES_DISPLAY_REQUIRED = 0x00000002,
     ES_SYSTEM_REQUIRED = 0x00000001
     // Legacy flag, should not be used.
     // ES_USER_PRESENT = 0x00000004
}
```

## Notes:
```cs
There is no need to store the state you set, Windows remembers it for you. Just set it back to ES_CONTINUOUS when you don't want it anymore.

Also note that this setting is per thread/application not global, so if you go to ES_CONTINUOUS and another app/thread is still setting ES_DISPLAY the   display will be kept on.
```

## Notes:
```cs
Note that the return value is the EXECUTION_STATE that ''was'' set.


Note ES_AWAYMODE_REQUIRED:
Although Away Mode is supported on any Windows Vista PC, the mode must be explicitly allowed by the current power policy. The Allow Away Mode power setting enables the user to selectively allow Away Mode on one or more power plans or individually for AC and DC (on battery) power states.
(see more about this at http://msdn.microsoft.com/en-us/windows/hardware/gg463208.aspx )
```

## Sample Code:
```cs
void PreventMonitorPowerdown ()
    {
        SetThreadExecutionState(EXECUTION_STATE.ES_DISPLAY_REQUIRED | EXECUTION_STATE.ES_CONTINUOUS);
    }

    void AllowMonitorPowerdown ()
    {
        SetThreadExecutionState(EXECUTION_STATE.ES_CONTINUOUS);
    }
```

## Sample Code:
```cs
void PreventSleep ()
    {
        // Prevent Idle-to-Sleep (monitor not affected) (see note above)
        SetThreadExecutionState(EXECUTION_STATE.ES_CONTINUOUS | EXECUTION_STATE.ES_AWAYMODE_REQUIRED);
    }

    void KeepSystemAwake ()
    {
        SetThreadExecutionState(EXECUTION_STATE.ES_SYSTEM_REQUIRED);
    }
```
