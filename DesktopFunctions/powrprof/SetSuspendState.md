
## C# Signature:
```cs
[DllImport ("Powrprof.dll", SetLastError = true)]
static extern uint SetSuspendState (bool hibernate, bool forceCritical, bool disableWakeEvent);
```

## VB Signature:
```cs
Declare Function SetSuspendState Lib "powrprof.dll" (ByVal Hibernate As Boolean, ByVal ForceCritical As Boolean, ByVal DisableWakeEvent As Boolean) As Boolean
```

## Sample Code:
```cs
using System.Runtime.InteropServices;

    namespace Sleeper
    {
        class Program
        {
            /// <summary>
            /// Suspends the system by shutting power down. Depending on the Hibernate parameter, the system either enters a suspend (sleep) state or hibernation (S4).
            /// </summary>
            /// <param name="hibernate">If this parameter is TRUE, the system hibernates. If the parameter is FALSE, the system is suspended.</param>
            /// <param name="forceCritical">Windows Server 2003, Windows XP, and Windows 2000:  If this parameter is TRUE, 
            /// the system suspends operation immediately; if it is FALSE, the system broadcasts a PBT_APMQUERYSUSPEND event to each 
            /// application to request permission to suspend operation.</param>
            /// <param name="disableWakeEvent">If this parameter is TRUE, the system disables all wake events. If the parameter is FALSE, any system wake events remain enabled.</param>
            /// <returns>If the function succeeds, the return value is true.</returns>
            /// <remarks>See http://msdn.microsoft.com/en-us/library/aa373201(VS.85).aspx</remarks>
            [DllImport("Powrprof.dll", SetLastError = true)]
            static extern uint SetSuspendState(bool hibernate, bool forceCritical, bool disableWakeEvent);

            static void Main(string[] args)
            {
                // Sleeps the machine
                SetSuspendState(false, false, false);
            }
        }
    }
```

## Sample Code:
```cs
Public Class Form1
```

## Sample Code:
```cs
Inherits System.Windows.Forms.Form

        'SetSuspendState will put the PC in to a standby mode
        Private Declare Function SetSuspendState Lib "powrprof.dll" (ByVal Hibernate As Boolean, ByVal ForceCritical As Boolean, _
        ByVal DisableWakeEvent As Boolean) As Boolean

        Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load
```

## Sample Code:
```cs
'SetSuspendState Example
        '*************************************************************************************************
        'SetSuspendState(False, False, False)
        '*************************************************************************************************

        End

        End Sub
```

## Alternative Managed API:
```cs
Application.SetSuspendState(PowerState.Hibernate, False, False)
    'Or
    Application.SetSuspendState(PowerState.Suspend, False, False)
```

## Alternative Managed API:
```cs
Member of System.Windows.Forms.Application
```
