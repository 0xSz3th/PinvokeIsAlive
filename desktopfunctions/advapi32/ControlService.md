
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError=true)]
[return: MarshalAs(UnmanagedType.Bool)]
public static extern bool    ControlService(IntPtr hService, SERVICE_CONTROL dwControl, ref SERVICE_STATUS lpServiceStatus);
```

## VB.Net Signature:
```cs
<DllImport("advapi32.dll", SetLastError:=True)> _
Public Function ControlService(ByVal hService As IntPtr, ByVal dwControl As SERVICE_CONTROL, ByRef lpServiceStatus As SERVICE_STATUS) As Boolean
End Function
```

## VB Signature:
```cs
Declare Function ControlService Lib "advapi32.dll" (ByVal hService As Long, ByVal lControlCode As Long, ByVal lpServiceStatus As SERVICE_STATUS) As Boolean
```

## C# User-Defined Types:
```cs
[Flags]
public enum SERVICE_CONTROL : uint
{
    STOP           = 0x00000001,
    PAUSE          = 0x00000002,
    CONTINUE           = 0x00000003,
    INTERROGATE        = 0x00000004,
    SHUTDOWN           = 0x00000005,
    PARAMCHANGE        = 0x00000006,
    NETBINDADD         = 0x00000007,
    NETBINDREMOVE      = 0x00000008,
    NETBINDENABLE      = 0x00000009,
    NETBINDDISABLE     = 0x0000000A,
    DEVICEEVENT        = 0x0000000B,
    HARDWAREPROFILECHANGE  = 0x0000000C,
    POWEREVENT         = 0x0000000D,
    SESSIONCHANGE      = 0x0000000E
}

public enum SERVICE_STATE : uint 
{
    SERVICE_STOPPED            = 0x00000001,
    SERVICE_START_PENDING          = 0x00000002,
    SERVICE_STOP_PENDING           = 0x00000003,
    SERVICE_RUNNING            = 0x00000004,
    SERVICE_CONTINUE_PENDING           = 0x00000005,
    SERVICE_PAUSE_PENDING          = 0x00000006,
    SERVICE_PAUSED             = 0x00000007
}

[Flags]
public enum SERVICE_ACCEPT : uint 
{
    STOP            = 0x00000001,
    PAUSE_CONTINUE      = 0x00000002,
    SHUTDOWN        = 0x00000004,
    PARAMCHANGE         = 0x00000008,
    NETBINDCHANGE       = 0x00000010,
    HARDWAREPROFILECHANGE   = 0x00000020,
    POWEREVENT          = 0x00000040,
    SESSIONCHANGE       = 0x00000080,
}
```

## VB User-Defined Types:
```cs
[STOP] = &H1
    PAUSE = &H2
    CONTINUE = &H3
    INTERROGATE = &H4
    SHUTDOWN = &H5
    PARAMCHANGE = &H6
    NETBINDADD = &H7
    NETBINDREMOVE = &H8
    NETBINDENABLE = &H9
    NETBINDDISABLE = &HA
    DEVICEEVENT = &HB
    HARDWAREPROFILECHANGE = &HC
    POWEREVENT = &HD
    SESSIONCHANGE = &HE
```

## VB User-Defined Types:
```cs
SERVICE_STOPPED = &H1
    SERVICE_START_PENDING = &H2
    SERVICE_STOP_PENDING = &H3
    SERVICE_RUNNING = &H4
    SERVICE_CONTINUE_PENDING = &H5
    SERVICE_PAUSE_PENDING = &H6
    SERVICE_PAUSED = &H7
```

## VB User-Defined Types:
```cs
[STOP] = &H1
    PAUSE_CONTINUE = &H2
    SHUTDOWN = &H4
    PARAMCHANGE = &H8
    NETBINDCHANGE = &H10
    HARDWAREPROFILECHANGE = &H20
    POWEREVENT = &H40
    SESSIONCHANGE = &H80
```

## Sample Code:
```cs
IntPtr con = Tools.OpenSCManager("\\\\compname", null, (uint)SCM_ACCESS.SC_MANAGER_ALL_ACCESS);
IntPtr serv = Tools.OpenService(con, "ServiceTest", (uint)SERVICE_ACCESS.SERVICE_ALL_ACCESS);
SERVICE_STATUS stat = new SERVICE_STATUS();
bool res = Tools.ControlService(m_serv, SERVICE_CONTROL.STOP, ref stat);
Console.WriteLine("Stop service result: " + res);
// TODO: Code to halt execution until the service has finally stopped, to continue another task afterwards.
```

## Alternative Managed API:
```cs
using System;
using System.Runtime.InteropServices;
using System.Reflection;
using System.ServiceProcess;
using System.Threading;


namespace ServiceHelper
{
     /// <summary>
     /// Helper class for service control.
     /// </summary>
     public class ServiceControl : IDisposable
     {
     private int WAIT_TIMEOUT = 0x00000102; 

     private IntPtr serviceControlManagerHandle;
     private IntPtr serviceHandle;
     private IntPtr statusHandle;

     private Thread heartbeatThread;

     private ManualResetEvent heartbeatStopped;
     private ManualResetEvent heartbeatActive;
     private ManualResetEvent terminationPending;

     private uint waitHintMilliseconds;
     private int heartbeatMilliseconds;

     public ServiceControl (ServiceBase aServiceBase, uint aWaitHintMilliseconds, int aHeartbeatMilliseconds)
     {
         FieldInfo fieldInfo;
         BindingFlags bindingFlags = BindingFlags.Instance | BindingFlags.NonPublic;
         SERVICE_STATUS serviceStatus;

         serviceControlManagerHandle = Interop.OpenSCManager (
         null, 
         null, 
         (uint) SCM_ACCESS.SC_MANAGER_ALL_ACCESS);

         if (serviceControlManagerHandle == IntPtr.Zero)
         {
         throw new Exception (aServiceBase.ServiceName);
         }

         serviceHandle = Interop.OpenService (
         serviceControlManagerHandle, 
         aServiceBase.ServiceName, 
        (uint) SERVICE_ACCESS.SERVICE_ALL_ACCESS);

         if (serviceHandle == IntPtr.Zero)
         {
         throw new Exception ("aServiceName");
         }

         fieldInfo = typeof (System.ServiceProcess.ServiceBase).GetField ("statusHandle", bindingFlags);

         statusHandle = (IntPtr) (fieldInfo.GetValue (aServiceBase));

         if (statusHandle == IntPtr.Zero)
         throw new Exception ("statusHandle is not valid.");

         waitHintMilliseconds = aWaitHintMilliseconds;
         heartbeatMilliseconds = aHeartbeatMilliseconds;

         serviceStatus = new SERVICE_STATUS ();

         Interop.QueryServiceStatus (serviceHandle, ref serviceStatus);
         serviceStatus.WaitHint = waitHintMilliseconds;
         Interop.SetServiceStatus (statusHandle, ref serviceStatus);

         terminationPending = new ManualResetEvent (false);
         heartbeatStopped = new ManualResetEvent (true);
         heartbeatActive = new ManualResetEvent (false);

         heartbeatThread = new Thread (IncrementHeartbeat);
         heartbeatThread.SetApartmentState (ApartmentState.MTA);
         heartbeatThread.Name = "Heartbeat_$" + Guid.NewGuid ().ToString ().Replace ('-', '_');

         heartbeatThread.Start ();
     }

     private SERVICE_STATUS DoQueryServiceStatus ()
     {
         SERVICE_STATUS serviceStatus = new SERVICE_STATUS();

         Interop.QueryServiceStatus (serviceHandle, ref serviceStatus);

         return serviceStatus;
     }


     public void StopHeartbeat ()
     {
         heartbeatActive.Reset ();
         heartbeatStopped.Set ();
     }

     public void StartHeartbeat ()
     {
         heartbeatStopped.Reset ();
         heartbeatActive.Set ();
     }

     private void IncrementHeartbeat ()
     {
         bool terminating = false;

         WaitHandle[] dispatchHandles = new WaitHandle[] { heartbeatStopped, heartbeatActive, terminationPending };
         WaitHandle[] activeHeartbeatHandles = new WaitHandle[] { heartbeatStopped, terminationPending };
         WaitHandle[] inactiveHeartbeatHandles = new WaitHandle[] { heartbeatActive, terminationPending };
         while (!terminating)
         {
         switch (WaitHandle.WaitAny (dispatchHandles))
         {
             case 0:
             WaitHandle.WaitAny (inactiveHeartbeatHandles);
             break;

             case 1:
             if (WaitHandle.WaitAny (activeHeartbeatHandles, heartbeatMilliseconds, false) == WAIT_TIMEOUT)
             {
                 SERVICE_STATUS serviceStatus = new SERVICE_STATUS ();

                 Interop.QueryServiceStatus (serviceHandle, ref serviceStatus);

                 serviceStatus.CheckPoint++;

                 Interop.SetServiceStatus (statusHandle, ref serviceStatus);
             }
             break;

         case 2: 
             terminating = true;
             heartbeatStopped.Set ();
             break;
         }
         }
     }

     private void DoControlService (SERVICE_CONTROL aServiceControl)
     {
         SERVICE_STATUS serviceStatus = new SERVICE_STATUS();

         if (!Interop.ControlService(serviceHandle, aServiceControl, ref serviceStatus))
         {
         throw new Exception (serviceStatus.ToString ());
         }  
     }

     public void Dispose()
     {
         heartbeatActive.Reset ();
         heartbeatStopped.Reset ();
         terminationPending.Set ();

         heartbeatStopped.WaitOne ();

         Interop.CloseServiceHandle (serviceHandle);
         Interop.CloseServiceHandle (serviceControlManagerHandle);
     }
     }

     public class TestService : ServiceBase
     {
     ServiceControl serviceControl;

     public static void Main ()
     {
         ServiceBase.Run (new TestService());
     }

     public TestService()
     {   
         InitializeComponent ();
     }

     protected override void OnPause ()
     {
         serviceControl = new ServiceControl (this, 60000, 10000);
         serviceControl.StartHeartbeat ();
         //TODO: Add pause code here ...
         serviceControl.StopHeartbeat ();
     }

     private void InitializeComponent()
     {
         this.CanPauseAndContinue = true;
         this.ServiceName = "TestService";
     }

     protected override void OnStop()
     {
         serviceControl = new ServiceControl (this, 60000, 10000);
         serviceControl.StartHeartbeat ();
         //TODO: Add stop code here ...
         serviceControl.StopHeartbeat ();        
     }
     } 

     internal class Interop
     {
     [DllImport ("advapi32.dll", SetLastError = true)]
     [return: MarshalAs (UnmanagedType.Bool)]
     internal static extern bool ControlService (
         IntPtr hService, 
         SERVICE_CONTROL dwControl, 
         ref SERVICE_STATUS lpServiceStatus);

     [DllImport ("advapi32.dll", EntryPoint = "OpenSCManagerW", ExactSpelling = true, CharSet = CharSet.Unicode, SetLastError = true)]
     internal static extern IntPtr OpenSCManager (
         string machineName, 
         string databaseName, 
         uint dwAccess);

     [DllImport ("advapi32.dll", SetLastError = true, CharSet = CharSet.Auto)]
     internal static extern IntPtr OpenService (IntPtr hSCManager, string lpServiceName, uint dwDesiredAccess);

     [DllImport ("advapi32.dll", SetLastError = true)]
     [return: MarshalAs (UnmanagedType.Bool)]
     internal static extern bool CloseServiceHandle (IntPtr hSCObject);

     [DllImport ("advapi32.dll", EntryPoint = "QueryServiceStatus", CharSet = CharSet.Auto)]
     internal static extern bool QueryServiceStatus (IntPtr hService, ref SERVICE_STATUS dwServiceStatus);

     [DllImport ("advapi32.dll")]
     internal static extern bool SetServiceStatus (IntPtr hServiceStatus, ref SERVICE_STATUS lpServiceStatus);
     }
}
```
