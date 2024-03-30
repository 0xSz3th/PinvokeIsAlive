
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError=true)]
[return: MarshalAs(UnmanagedType.Bool)]
public static extern bool DeleteService( IntPtr hService );
```

## VB.Net Signature:
```cs
<DllImport("advapi32.dll", SetLastError:=True)> _
Public Function DeleteService(ByVal hService As IntPtr) As Boolean
End Function
```

## VB Signature:
```cs
Declare Function DeleteService Lib "advapi32.dll" (ByVal hService As Integer) As Integer
```

## Sample Code:
```cs
#region SERVICE_ACCESS
    [Flags]
    public enum SERVICE_ACCESS : uint
    {
        STANDARD_RIGHTS_REQUIRED   = 0xF0000,
        SERVICE_QUERY_CONFIG       = 0x00001,
        SERVICE_CHANGE_CONFIG      = 0x00002,
        SERVICE_QUERY_STATUS       = 0x00004,
        SERVICE_ENUMERATE_DEPENDENTS   = 0x00008,
        SERVICE_START      = 0x00010,
        SERVICE_STOP       = 0x00020,
        SERVICE_PAUSE_CONTINUE     = 0x00040,
        SERVICE_INTERROGATE    = 0x00080,
        SERVICE_USER_DEFINED_CONTROL   = 0x00100,
        SERVICE_ALL_ACCESS     = (STANDARD_RIGHTS_REQUIRED     | 
            SERVICE_QUERY_CONFIG     | 
            SERVICE_CHANGE_CONFIG    | 
            SERVICE_QUERY_STATUS     | 
            SERVICE_ENUMERATE_DEPENDENTS | 
            SERVICE_START    | 
            SERVICE_STOP     | 
            SERVICE_PAUSE_CONTINUE       | 
            SERVICE_INTERROGATE      | 
            SERVICE_USER_DEFINED_CONTROL)
    }
    #endregion
    #region SCM_ACCESS
    [Flags]
    public enum SCM_ACCESS : uint
    {
        STANDARD_RIGHTS_REQUIRED       = 0xF0000,
        SC_MANAGER_CONNECT     = 0x00001,
        SC_MANAGER_CREATE_SERVICE      = 0x00002,
        SC_MANAGER_ENUMERATE_SERVICE   = 0x00004,
        SC_MANAGER_LOCK    = 0x00008,
        SC_MANAGER_QUERY_LOCK_STATUS   = 0x00010,
        SC_MANAGER_MODIFY_BOOT_CONFIG  = 0x00020,
        SC_MANAGER_ALL_ACCESS      = STANDARD_RIGHTS_REQUIRED |
            SC_MANAGER_CONNECT |
            SC_MANAGER_CREATE_SERVICE |
            SC_MANAGER_ENUMERATE_SERVICE |
            SC_MANAGER_LOCK |
            SC_MANAGER_QUERY_LOCK_STATUS |
            SC_MANAGER_MODIFY_BOOT_CONFIG
    }
    #endregion

        #region DeleteService
        [DllImport("advapi32.dll", SetLastError=true)]
        [return: MarshalAs(UnmanagedType.Bool)]
        public static extern bool DeleteService( IntPtr hService );
        #endregion
        #region OpenService
        [DllImport("advapi32.dll", SetLastError=true, CharSet=CharSet.Auto)]
        static extern IntPtr OpenService(IntPtr hSCManager, string lpServiceName, SERVICE_ACCESS dwDesiredAccess);
        #endregion
        #region OpenSCManager
        [DllImport("advapi32.dll", EntryPoint="OpenSCManagerW", ExactSpelling=true, CharSet=CharSet.Unicode, SetLastError=true)]
        static extern IntPtr OpenSCManager( string machineName, string databaseName, SCM_ACCESS dwDesiredAccess );
        #endregion
        #region CloseServiceHandle
        [DllImport("advapi32.dll", SetLastError=true)]
        [return: MarshalAs(UnmanagedType.Bool)]
        static extern bool CloseServiceHandle( IntPtr hSCObject );
        #endregion

            try
            {
                IntPtr schSCManager = OpenSCManager( null, null, SCM_ACCESS.SC_MANAGER_ALL_ACCESS);
                if( schSCManager != IntPtr.Zero )
                {
                    IntPtr schService = OpenService( schSCManager, txtServiceName.Text, SERVICE_ACCESS.SERVICE_ALL_ACCESS);
                    if( schService != IntPtr.Zero )
                    {
                        if(DeleteService( schService )== false)
                        {
                            MessageBox.Show(
                                string.Format("DeleteService failed {0}",Marshal.GetLastWin32Error()));
                        }
                    }
                    CloseServiceHandle( schSCManager );
                    // if you don't close this handle, Services control panel
                    // shows the service as "disabled", and you'll get 1072 errors
                    // trying to reuse this service's name
                    CloseServiceHandle( schService );

                }
            }
            catch (System.Exception ex)
            {
                MessageBox.Show(ex.Message);
            }
```
