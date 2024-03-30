
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError=true, CharSet=CharSet.Auto)]
static extern IntPtr CreateService(
    IntPtr hSCManager,
    string lpServiceName,
    string lpDisplayName,
    uint dwDesiredAccess,
    uint dwServiceType,
    uint dwStartType,
    uint dwErrorControl,
    string lpBinaryPathName,
    [Optional] string lpLoadOrderGroup,
    [Optional] string lpdwTagId,    // only string so we can pass null
    [Optional] string lpDependencies,
    [Optional] string lpServiceStartName,
    [Optional] string lpPassword);
```

## VB Signature:
```cs
<DllImport("advapi32.dll", SetLastError:=True, CharSet:=CharSet.Auto)> _
    Private Shared Function CreateService(ByVal hSCManager As IntPtr, ByVal serviceName As String, _
                ByVal displayName As String, ByVal desiredAccess As Int32, ByVal serviceType As Int32, _
                ByVal startType As Int32, ByVal errorcontrol As Int32, ByVal binaryPathName As String, _
                ByVal loadOrderGroup As String, ByVal TagBY As Int32, ByVal dependencides As String, _
                ByVal serviceStartName As String, ByVal password As String) As IntPtr
```

## C# User-Defined Types:
```cs
/// <summary>
    /// Access to the service. Before granting the requested access, the
    /// system checks the access token of the calling process. 
    /// </summary>
   [Flags]
    public enum SERVICE_ACCESS : uint
    {
    /// <summary>
    /// Required to call the QueryServiceConfig and 
    /// QueryServiceConfig2 functions to query the service configuration.
    /// </summary>
    SERVICE_QUERY_CONFIG = 0x00001,

    /// <summary>
    /// Required to call the ChangeServiceConfig or ChangeServiceConfig2 function 
    /// to change the service configuration. Because this grants the caller 
    /// the right to change the executable file that the system runs, 
    /// it should be granted only to administrators.
    /// </summary>
    SERVICE_CHANGE_CONFIG = 0x00002,

    /// <summary>
    /// Required to call the QueryServiceStatusEx function to ask the service 
    /// control manager about the status of the service.
    /// </summary>
    SERVICE_QUERY_STATUS = 0x00004,

    /// <summary>
    /// Required to call the EnumDependentServices function to enumerate all 
    /// the services dependent on the service.
    /// </summary>
    SERVICE_ENUMERATE_DEPENDENTS = 0x00008,

    /// <summary>
    /// Required to call the StartService function to start the service.
    /// </summary>
    SERVICE_START = 0x00010,

    /// <summary>
    ///     Required to call the ControlService function to stop the service.
    /// </summary>
    SERVICE_STOP = 0x00020,

    /// <summary>
    /// Required to call the ControlService function to pause or continue 
    /// the service.
    /// </summary>
    SERVICE_PAUSE_CONTINUE = 0x00040,

    /// <summary>
    /// Required to call the EnumDependentServices function to enumerate all
    /// the services dependent on the service.
    /// </summary>
    SERVICE_INTERROGATE = 0x00080,

    /// <summary>
    /// Required to call the ControlService function to specify a user-defined
    /// control code.
    /// </summary>
    SERVICE_USER_DEFINED_CONTROL = 0x00100,

    /// <summary>
    /// Includes STANDARD_RIGHTS_REQUIRED in addition to all access rights in this table.
    /// </summary>
    SERVICE_ALL_ACCESS = (ACCESS_MASK.STANDARD_RIGHTS_REQUIRED |
        SERVICE_QUERY_CONFIG |
        SERVICE_CHANGE_CONFIG |
        SERVICE_QUERY_STATUS |
        SERVICE_ENUMERATE_DEPENDENTS |
        SERVICE_START |
        SERVICE_STOP |
        SERVICE_PAUSE_CONTINUE |
        SERVICE_INTERROGATE |
        SERVICE_USER_DEFINED_CONTROL),

    GENERIC_READ = ACCESS_MASK.STANDARD_RIGHTS_READ |
        SERVICE_QUERY_CONFIG |
        SERVICE_QUERY_STATUS |
        SERVICE_INTERROGATE |
        SERVICE_ENUMERATE_DEPENDENTS,

    GENERIC_WRITE = ACCESS_MASK.STANDARD_RIGHTS_WRITE |
        SERVICE_CHANGE_CONFIG,

    GENERIC_EXECUTE = ACCESS_MASK.STANDARD_RIGHTS_EXECUTE |
        SERVICE_START |
        SERVICE_STOP |
        SERVICE_PAUSE_CONTINUE |
        SERVICE_USER_DEFINED_CONTROL,

    /// <summary>
    /// Required to call the QueryServiceObjectSecurity or 
    /// SetServiceObjectSecurity function to access the SACL. The proper
    /// way to obtain this access is to enable the SE_SECURITY_NAME 
    /// privilege in the caller's current access token, open the handle 
    /// for ACCESS_SYSTEM_SECURITY access, and then disable the privilege.
    /// </summary>
    ACCESS_SYSTEM_SECURITY = ACCESS_MASK.ACCESS_SYSTEM_SECURITY,

    /// <summary>
    /// Required to call the DeleteService function to delete the service.
    /// </summary>
    DELETE = ACCESS_MASK.DELETE,

    /// <summary>
    /// Required to call the QueryServiceObjectSecurity function to query
    /// the security descriptor of the service object.
    /// </summary>
    READ_CONTROL = ACCESS_MASK.READ_CONTROL,

    /// <summary>
    /// Required to call the SetServiceObjectSecurity function to modify
    /// the Dacl member of the service object's security descriptor.
    /// </summary>
    WRITE_DAC = ACCESS_MASK.WRITE_DAC,

    /// <summary>
    /// Required to call the SetServiceObjectSecurity function to modify 
    /// the Owner and Group members of the service object's security 
    /// descriptor.
    /// </summary>
    WRITE_OWNER = ACCESS_MASK.WRITE_OWNER,
    }

    /// <summary>
    /// Service types.
    /// </summary>
    [Flags]
    public enum SERVICE_TYPE : uint
    {
    /// <summary>
    /// Driver service.
    /// </summary>
    SERVICE_KERNEL_DRIVER = 0x00000001,

    /// <summary>
    /// File system driver service.
    /// </summary>
    SERVICE_FILE_SYSTEM_DRIVER = 0x00000002,

    /// <summary>
    /// Service that runs in its own process.
    /// </summary>
    SERVICE_WIN32_OWN_PROCESS = 0x00000010,

    /// <summary>
    /// Service that shares a process with one or more other services.
    /// </summary>
    SERVICE_WIN32_SHARE_PROCESS = 0x00000020,

    /// <summary>
    /// The service can interact with the desktop.
    /// </summary>
    SERVICE_INTERACTIVE_PROCESS = 0x00000100,
    }

    /// <summary>
    /// Service start options
    /// </summary>
    public enum SERVICE_START : uint
    {     
    /// <summary>
    /// A device driver started by the system loader. This value is valid
    /// only for driver services.
    /// </summary>
    SERVICE_BOOT_START = 0x00000000,

    /// <summary>
    /// A device driver started by the IoInitSystem function. This value 
    /// is valid only for driver services.
    /// </summary>
    SERVICE_SYSTEM_START = 0x00000001,

    /// <summary>
    /// A service started automatically by the service control manager 
    /// during system startup. For more information, see Automatically 
    /// Starting Services.
    /// </summary>         
    SERVICE_AUTO_START = 0x00000002,

    /// <summary>
    /// A service started by the service control manager when a process 
    /// calls the StartService function. For more information, see 
    /// Starting Services on Demand.
    /// </summary>
    SERVICE_DEMAND_START = 0x00000003,

    /// <summary>
    /// A service that cannot be started. Attempts to start the service
    /// result in the error code ERROR_SERVICE_DISABLED.
    /// </summary>
    SERVICE_DISABLED = 0x00000004,       
    }
```

## C# User-Defined Types:
```cs
/// <summary>
    /// Severity of the error, and action taken, if this service fails 
    /// to start.
    /// </summary>
    public enum SERVICE_ERROR 
    {       
    /// <summary>
    /// The startup program ignores the error and continues the startup
    /// operation.
    /// </summary>
    SERVICE_ERROR_IGNORE = 0x00000000,

    /// <summary>
    /// The startup program logs the error in the event log but continues
    /// the startup operation.
    /// </summary>
    SERVICE_ERROR_NORMAL = 0x00000001,

    /// <summary>
    /// The startup program logs the error in the event log. If the 
    /// last-known-good configuration is being started, the startup 
    /// operation continues. Otherwise, the system is restarted with 
    /// the last-known-good configuration.
    /// </summary>
    SERVICE_ERROR_SEVERE = 0x00000002,

    /// <summary>
    /// The startup program logs the error in the event log, if possible.
    /// If the last-known-good configuration is being started, the startup
    /// operation fails. Otherwise, the system is restarted with the 
    /// last-known good configuration.
    /// </summary>
    SERVICE_ERROR_CRITICAL = 0x00000003,
    }
```

## VB.NET User-Defined Types:
```cs
Public Enum SERVICE_ERROR
    ''' <summary>
    ''' The startup program ignores the error and continues the startup
    ''' operation.
    ''' </summary>
    SERVICE_ERROR_IGNORE = 0

    ''' <summary>
    ''' The startup program logs the error in the event log but continues
    ''' the startup operation.
    ''' </summary>
    SERVICE_ERROR_NORMAL = 1

    ''' <summary>
    ''' The startup program logs the error in the event log. If the 
    ''' last-known-good configuration is being started, the startup 
    ''' operation continues. Otherwise, the system is restarted with 
    ''' the last-known-good configuration.
    ''' </summary>
    SERVICE_ERROR_SEVERE = 2

    ''' <summary>
    ''' The startup program logs the error in the event log, if possible.
    ''' If the last-known-good configuration is being started, the startup
    ''' operation fails. Otherwise, the system is restarted with the 
    ''' last-known good configuration.
    ''' </summary>
    SERVICE_ERROR_CRITICAL = 3

    End Enum

    ''' <summary>
    ''' Access to the service. Before granting the requested access, the
    ''' system checks the access token of the calling process. 
    ''' </summary>
    <Flags()> _
    Public Enum SERVICE_ACCESS As UInteger
    ''' <summary>
    ''' Required to call the QueryServiceConfig and 
    ''' QueryServiceConfig2 functions to query the service configuration.
    ''' </summary>
    SERVICE_QUERY_CONFIG = &H1

    ''' <summary>
    ''' Required to call the ChangeServiceConfig or ChangeServiceConfig2 function 
    ''' to change the service configuration. Because this grants the caller 
    ''' the right to change the executable file that the system runs 
    ''' it should be granted only to administrators.
    ''' </summary>
    SERVICE_CHANGE_CONFIG = &H2

    ''' <summary>
    ''' Required to call the QueryServiceStatusEx function to ask the service 
    ''' control manager about the status of the service.
    ''' </summary>
    SERVICE_QUERY_STATUS = &H4

    ''' <summary>
    ''' Required to call the EnumDependentServices function to enumerate all 
    ''' the services dependent on the service.
    ''' </summary>
    SERVICE_ENUMERATE_DEPENDENTS = &H8

    ''' <summary>
    ''' Required to call the StartService function to start the service.
    ''' </summary>
    SERVICE_START = &H10

    ''' <summary>
    '''     Required to call the ControlService function to stop the service.
    ''' </summary>
    SERVICE_STOP = &H20

    ''' <summary>
    ''' Required to call the ControlService function to pause or continue 
    ''' the service.
    ''' </summary>
    SERVICE_PAUSE_CONTINUE = &H40

    ''' <summary>
    ''' Required to call the EnumDependentServices function to enumerate all
    ''' the services dependent on the service.
    ''' </summary>
    SERVICE_INTERROGATE = &H80

    ''' <summary>
    ''' Required to call the ControlService function to specify a user-defined
    ''' control code.
    ''' </summary>
    SERVICE_USER_DEFINED_CONTROL = &H100

    ''' <summary>
    ''' Includes STANDARD_RIGHTS_REQUIRED in addition to all access rights in this table.
    ''' </summary>
    SERVICE_ALL_ACCESS = (ACCESS_MASK.STANDARD_RIGHTS_REQUIRED Or _
        SERVICE_QUERY_CONFIG Or _
        SERVICE_CHANGE_CONFIG Or _
        SERVICE_QUERY_STATUS Or _
        SERVICE_ENUMERATE_DEPENDENTS Or _
        SERVICE_START Or _
        SERVICE_STOP Or _
        SERVICE_PAUSE_CONTINUE Or _
        SERVICE_INTERROGATE Or _
        SERVICE_USER_DEFINED_CONTROL)

    GENERIC_READ = ACCESS_MASK.STANDARD_RIGHTS_READ Or _
        SERVICE_QUERY_CONFIG Or _
        SERVICE_QUERY_STATUS Or _
        SERVICE_INTERROGATE Or _
        SERVICE_ENUMERATE_DEPENDENTS

    GENERIC_WRITE = ACCESS_MASK.STANDARD_RIGHTS_WRITE Or _
    SERVICE_CHANGE_CONFIG

    GENERIC_EXECUTE = ACCESS_MASK.STANDARD_RIGHTS_EXECUTE Or _
        SERVICE_START Or _
        SERVICE_STOP Or _
        SERVICE_PAUSE_CONTINUE Or _
        SERVICE_USER_DEFINED_CONTROL

    ''' <summary>
    ''' Required to call the QueryServiceObjectSecurity or 
    ''' SetServiceObjectSecurity function to access the SACL. The proper
    ''' way to obtain this access is to enable the SE_SECURITY_NAME 
    ''' privilege in the caller's current access token open the handle 
    ''' for ACCESS_SYSTEM_SECURITY access and then disable the privilege.
    ''' </summary>
    ACCESS_SYSTEM_SECURITY = ACCESS_MASK.ACCESS_SYSTEM_SECURITY

    ''' <summary>
    ''' Required to call the DeleteService function to delete the service.
    ''' </summary>
    DELETE = ACCESS_MASK.DELETE

    ''' <summary>
    ''' Required to call the QueryServiceObjectSecurity function to query
    ''' the security descriptor of the service object.
    ''' </summary>
    READ_CONTROL = ACCESS_MASK.READ_CONTROL

    ''' <summary>
    ''' Required to call the SetServiceObjectSecurity function to modify
    ''' the Dacl member of the service object's security descriptor.
    ''' </summary>
    WRITE_DAC = ACCESS_MASK.WRITE_DAC

    ''' <summary>
    ''' Required to call the SetServiceObjectSecurity function to modify 
    ''' the Owner and Group members of the service object's security 
    ''' descriptor.
    ''' </summary>
    WRITE_OWNER = ACCESS_MASK.WRITE_OWNER
    End Enum

    ''' <summary>
    ''' Service types.
    ''' </summary>
    <Flags()> _
    Public Enum SERVICE_TYPE As UInteger
    ''' <summary>
    ''' Driver service.
    ''' </summary>
    SERVICE_KERNEL_DRIVER = &H1

    ''' <summary>
    ''' File system driver service.
    ''' </summary>
    SERVICE_FILE_SYSTEM_DRIVER = &H2

    ''' <summary>
    ''' Service that runs in its own process.
    ''' </summary>
    SERVICE_WIN32_OWN_PROCESS = &H10

    ''' <summary>
    ''' Service that shares a process with one or more other services.
    ''' </summary>
    SERVICE_WIN32_SHARE_PROCESS = &H20

    ''' <summary>
    ''' The service can interact with the desktop.
    ''' </summary>
    SERVICE_INTERACTIVE_PROCESS = &H100
    End Enum

    ''' <summary>
    ''' Service start options
    ''' </summary>
    Public Enum SERVICE_START As UInteger
    ''' <summary>
    ''' A device driver started by the system loader. This value is valid
    ''' only for driver services.
    ''' </summary>
    SERVICE_BOOT_START = &H0

    ''' <summary>
    ''' A device driver started by the IoInitSystem function. This value 
    ''' is valid only for driver services.
    ''' </summary>
    SERVICE_SYSTEM_START = &H1

    ''' <summary>
    ''' A service started automatically by the service control manager 
    ''' during system startup. For more information, see Automatically 
    ''' Starting Services.
    ''' </summary>     
    SERVICE_AUTO_START = &H2

    ''' <summary>
    ''' A service started by the service control manager when a process 
    ''' calls the StartService function. For more information, see 
    ''' Starting Services on Demand.
    ''' </summary>
    SERVICE_DEMAND_START = &H3

    ''' <summary>
    ''' A service that cannot be started. Attempts to start the service
    ''' result in the error code ERROR_SERVICE_DISABLED.
    ''' </summary>
    SERVICE_DISABLED = &H4
    End Enum
```

## Sample Code:
```cs
Dim scHandle As IntPtr = OpenSCManager(Nothing, Nothing, SC_MANAGER_ALL_ACCESS)
    Dim serviceName As String = "AAATestService"
    Dim displayName As String = "AAATestDisplayName"

    If OpenFileDialog1.ShowDialog() <> DialogResult.OK Then
        MsgBox("aborting")
    End If

    Dim pathName As String = Chr(34) & OpenFileDialog1.FileName & Chr(34)

    Dim serviceHandle As IntPtr = CreateService(scHandle, serviceName, displayName, SERVICE_ALL_ACCESS, SERVICE_WIN32_OWN_PROCESS, _
                SERVICE_AUTO_START, SERVICE_ERROR_NORMAL, pathName, Nothing, 0, Nothing, Nothing, Nothing)
    If serviceHandle.Equals(IntPtr.Zero) Then
        MsgBox(Marshal.GetLastWin32Error())
    End If

    CloseServiceHandle(serviceHandle)
    CloseHandle(scHandle)
```
