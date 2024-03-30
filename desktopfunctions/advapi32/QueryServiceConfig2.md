
## C# Signature:
```cs
[DllImport( "advapi32.dll", CharSet = CharSet.Unicode, SetLastError = true, EntryPoint = "QueryServiceConfig2W" )]
public static extern Boolean QueryServiceConfig2( IntPtr hService, UInt32 dwInfoLevel, IntPtr buffer, UInt32 cbBufSize, out UInt32 pcbBytesNeeded );
```

## VB Signature:
```cs
Declare Function QueryServiceConfig2 Lib "advapi32.dll" (TODO) As TODO
```

## Sample Code:
```cs
static void Main( string [] args )
    {
        // Use the service name and *NOT* the display name.
        string serviceName = "Dnscache"; // Display name is "DNS Client"
        if ( args.Length > 0 )
            serviceName = args [ 0 ];
        IntPtr databaseHandle = OpenSCManager( null, null, SC_MANAGER_ALL_ACCESS );
        if ( databaseHandle == IntPtr.Zero )
            throw new System.Runtime.InteropServices.ExternalException( "Error OpenSCManager\n" );

        IntPtr serviceHandle = OpenService( databaseHandle, serviceName, SERVICE_QUERY_CONFIG );
        if ( serviceHandle == IntPtr.Zero )
            throw new System.Runtime.InteropServices.ExternalException( "Error OpenService\n" );

        ReportDescription( serviceHandle );
        ReportFailureActions( serviceHandle );
    }

    static private void ReportDescription( IntPtr serviceHandle )
    {
        UInt32 dwBytesNeeded;

        // Determine the buffer size needed
        bool sucess = QueryServiceConfig2( serviceHandle, SERVICE_CONFIG_DESCRIPTION, IntPtr.Zero, 0, out dwBytesNeeded );

        IntPtr ptr = Marshal.AllocHGlobal( ( int )dwBytesNeeded );
        sucess = QueryServiceConfig2( serviceHandle, SERVICE_CONFIG_DESCRIPTION, ptr, dwBytesNeeded, out dwBytesNeeded );
        SERVICE_DESCRIPTION descriptionStruct = new SERVICE_DESCRIPTION();
        Marshal.PtrToStructure( ptr, descriptionStruct );
        Marshal.FreeHGlobal( ptr );

        // Report it.
        Console.WriteLine( descriptionStruct.lpDescription );
    }

    static private void ReportFailureActions( IntPtr serviceHandle )
    {
        UInt32 dwBytesNeeded;
        const UInt32 INFINITE = 0xFFFFFFFF;

        // Determine the buffer size needed
        bool sucess = QueryServiceConfig2( serviceHandle, SERVICE_CONFIG_FAILURE_ACTIONS, IntPtr.Zero, 0, out dwBytesNeeded );

        IntPtr ptr = Marshal.AllocHGlobal( ( int )dwBytesNeeded );
        sucess = QueryServiceConfig2( serviceHandle, SERVICE_CONFIG_FAILURE_ACTIONS, ptr, dwBytesNeeded, out dwBytesNeeded );
        SERVICE_FAILURE_ACTIONS failureActions = new SERVICE_FAILURE_ACTIONS();
        Marshal.PtrToStructure( ptr, failureActions );

        // Report it.
        Console.WriteLine( "Reset Period: {0}", ( UInt32 )failureActions.dwResetPeriod != INFINITE 
            ? failureActions.dwResetPeriod.ToString() : "INFINITE" );
        Console.WriteLine( "Reboot message: {0}", failureActions.lpRebootMsg );
        Console.WriteLine( "Command line: {0}", failureActions.lpCommand );
        Console.WriteLine( "Number of actions: {0}", failureActions.cActions );

        SC_ACTION [] actions = new SC_ACTION [ failureActions.cActions ];
        int offset = 0;
        for ( int i = 0; i < failureActions.cActions; i++ )
        {
            SC_ACTION action = new SC_ACTION();
            action.type = Marshal.ReadInt32( failureActions.lpsaActions, offset );
            offset += sizeof( Int32 );
            action.dwDelay = ( UInt32 )Marshal.ReadInt32( failureActions.lpsaActions, offset );
            offset += sizeof( Int32 );
            actions [ i ] = action;
        }

        Marshal.FreeHGlobal( ptr );

        foreach ( SC_ACTION action in actions )
        {
            Console.WriteLine( "Type: {0}, Delay (msec): {1}", action.type, action.dwDelay );
        }
    }

    #region P/Invoke declarations
    [StructLayout( LayoutKind.Sequential )]
    public class SERVICE_DESCRIPTION
    {
        [MarshalAs( System.Runtime.InteropServices.UnmanagedType.LPWStr )]
        public String lpDescription;
    }

    [StructLayout( LayoutKind.Sequential, CharSet = CharSet.Unicode )]
    public class SERVICE_FAILURE_ACTIONS
    {
        public int dwResetPeriod;
        [MarshalAs( UnmanagedType.LPWStr )]
        public string lpRebootMsg;
        [MarshalAs( UnmanagedType.LPWStr )]
        public string lpCommand;
        public int cActions;
        public IntPtr lpsaActions;
    }

    [StructLayout( LayoutKind.Sequential )]
    public class SC_ACTION
    {
        public Int32 type;
        public UInt32 dwDelay;
    }

    [DllImport( "advapi32.dll", CharSet = CharSet.Unicode, SetLastError = true )]
    public static extern IntPtr OpenSCManager( String lpMachineName, String lpDatabaseName, UInt32 dwDesiredAccess );
    [DllImport( "advapi32.dll", CharSet = CharSet.Unicode, SetLastError = true )]
    public static extern IntPtr OpenService( IntPtr hSCManager, String lpServiceName, UInt32 dwDesiredAccess );
    [DllImport( "advapi32.dll", CharSet = CharSet.Unicode, SetLastError = true, EntryPoint = "QueryServiceConfig2W" )]
    public static extern Boolean QueryServiceConfig2( IntPtr hService, UInt32 dwInfoLevel, IntPtr buffer, UInt32 cbBufSize, out UInt32 pcbBytesNeeded );

    private const Int32 SC_MANAGER_ALL_ACCESS = 0x000F003F;
    private const Int32 SERVICE_QUERY_CONFIG = 0x00000001;
    private const UInt32 SERVICE_CONFIG_DESCRIPTION = 0x01;
    private const UInt32 SERVICE_CONFIG_FAILURE_ACTIONS = 0x02;

    #endregion // P/Invoke declarations
```
