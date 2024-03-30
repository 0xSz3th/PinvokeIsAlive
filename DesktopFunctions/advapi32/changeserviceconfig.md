
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError=true, CharSet=CharSet.Auto)]
    [return: MarshalAs(UnmanagedType.Bool)]
    public static extern bool ChangeServiceConfig2(
        IntPtr hService, 
        int dwInfoLevel,
        IntPtr lpInfo);
```

## Better C# Signature:
```cs
[DllImport("advapi32.dll", EntryPoint = "ChangeServiceConfig")]
    [return: MarshalAs(UnmanagedType.Bool)]
    public static extern bool ChangeServiceConfigA(IntPtr hService, uint dwServiceType,
    int dwStartType, int dwErrorControl, string lpBinaryPathName, string lpLoadOrderGroup,
    string lpdwTagId, string lpDependencies, string lpServiceStartName, string lpPassword,
    string lpDisplayName);
```

## VB Signature:
```cs
Declare Function ChangeServiceConfig2 Lib "advapi32.dll" (TODO) As TODO
```

## Notes:
```cs
1    SERVICE_CONFIG_DESCRIPTION
2    SERVICE_CONFIG_FAILURE_ACTIONS
3    SERVICE_CONFIG_DELAYED_AUTO_START_INFO
4    SERVICE_CONFIG_FAILURE_ACTIONS_FLAG
5    SERVICE_CONFIG_SERVICE_SID_INFO
6    SERVICE_CONFIG_REQUIRED_PRIVILEGES_INFO
7    SERVICE_CONFIG_PRESHUTDOWN_INFO
```

## Sample Code:
```cs
public MyServiceInstaller()
    {
        InitializeComponent();
        serviceInstaller1.Committed += new InstallEventHandler(serviceInstaller1_Committed);
    }

    void serviceInstaller1_Committed(object sender, InstallEventArgs e)
    {
        IntPtr scHandle = IntPtr.Zero;
        IntPtr svcHandle = IntPtr.Zero;
        string serviceName = "MyService";

        try
        {
        scHandle = OpenSCManager(null, null, (uint)SCM_ACCESS.SC_MANAGER_ALL_ACCESS);
        if (scHandle == IntPtr.Zero)
        {
            throw new Exception(String.Format("Error connecting to Service Control Manager. Error provided was: 0x{0:X}", Marshal.GetLastWin32Error()));
        }

        svcHandle = OpenService(scHandle, serviceName, (int)SERVICE_ACCESS.SERVICE_ALL_ACCESS);
        if (svcHandle == IntPtr.Zero)
        {
            throw new Exception(String.Format("Error opening service for modifying. Error returned was: 0x{0:X}", Marshal.GetLastWin32Error()));
        }

        SC_ACTION action = new SC_ACTION();
        action.Type = SC_ACTION_RESTART;
        action.Delay = (int)TimeSpan.FromMinutes(1).TotalMilliseconds;

        IntPtr lpsaActions = Marshal.AllocHGlobal(Marshal.SizeOf(action) * 2);
        if (lpsaActions == IntPtr.Zero)
        {
            throw new Exception(String.Format("Unable to allocate memory for service action, error was: 0x{0:X}", Marshal.GetLastWin32Error()));
        }

        Marshal.StructureToPtr(action, lpsaActions, false);

        IntPtr nextAction = (IntPtr)(lpsaActions.ToInt64() + Marshal.SizeOf(action));
        action.Type = SC_ACTION_NONE;

        Marshal.StructureToPtr(action, nextAction, false);

        SERVICE_FAILURE_ACTIONS failureActions = new SERVICE_FAILURE_ACTIONS();
        failureActions.dwResetPeriod = (int)TimeSpan.FromDays(1).TotalSeconds;
        failureActions.lpRebootMsg = "";
        failureActions.lpCommand = "";
        failureActions.cActions = 2;
        failureActions.lpsaActions = lpsaActions;

        IntPtr lpInfo = Marshal.AllocHGlobal(Marshal.SizeOf(failureActions));
        if (lpInfo == IntPtr.Zero)
        {
            Marshal.FreeHGlobal(lpsaActions);
            throw new Exception(String.Format("Unable to allocate memory, error was: 0x{0:X}", Marshal.GetLastWin32Error()));
        }

        Marshal.StructureToPtr(failureActions, lpInfo, false);

        if (!ChangeServiceConfig2(svcHandle, SERVICE_CONFIG_FAILURE_ACTIONS, lpInfo))
        {
            Marshal.FreeHGlobal(lpInfo);
            Marshal.FreeHGlobal(lpsaActions);
            throw new Exception(String.Format("Error setting service config, error was: 0x{0:X}", Marshal.GetLastWin32Error()));
        }

        Marshal.FreeHGlobal(lpInfo);
        Marshal.FreeHGlobal(lpsaActions);

        EventLog.WriteEntry("MyService", "Service modification completed");
        }
        catch (Exception ex)
        {
        EventLog.WriteEntry("MyService", ex.Message);
        }

        // Make sure to close open handles
        if (svcHandle != IntPtr.Zero)
        {
        CloseServiceHandle(svcHandle);
        }

        if (scHandle != IntPtr.Zero)
        {
        CloseServiceHandle(scHandle);
        }
    }
```
