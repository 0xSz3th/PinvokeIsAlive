
## C# Signature:
```cs
[DllImport("ntdll.dll", SetLastError = true)]
    public static extern IntPtr RtlAdjustPrivilege(int Privilege, bool bEnablePrivilege,
    bool IsThreadPrivilege, out bool PreviousValue);
```

## with Privilege enum
```cs
[DllImport("ntdll.dll", SetLastError = true)]
    public static extern IntPtr RtlAdjustPrivilege(Privilege privilege, bool bEnablePrivilege,
    bool IsThreadPrivilege, out bool PreviousValue);
```

## VB Signature:
```cs
<DllImport("ntdll.dll")>
    Public Shared Function RtlAdjustPrivilege(ByVal Privilege As Integer, ByVal bEnablePrivilege As Boolean, ByVal IsThreadPrivilege As Boolean, <Out> ByRef PreviousValue As Boolean) As UInteger
    End Function
```

## C/C++:
```cs
(
  ULONG    Privilege,
  BOOLEAN  Enable,
  BOOLEAN  CurrentThread,
  PBOOLEAN Enabled
```

## C# Privilege enum : (added by Lufzys)
```cs
public enum Privilege : int
    {
        SeCreateTokenPrivilege = 1,
        SeAssignPrimaryTokenPrivilege = 2,
        SeLockMemoryPrivilege = 3,
        SeIncreaseQuotaPrivilege = 4,
        SeUnsolicitedInputPrivilege = 5,
        SeMachineAccountPrivilege = 6,
        SeTcbPrivilege = 7,
        SeSecurityPrivilege = 8,
        SeTakeOwnershipPrivilege = 9,
        SeLoadDriverPrivilege = 10,
        SeSystemProfilePrivilege = 11,
        SeSystemtimePrivilege = 12,
        SeProfileSingleProcessPrivilege = 13,
        SeIncreaseBasePriorityPrivilege = 14,
        SeCreatePagefilePrivilege = 15,
        SeCreatePermanentPrivilege = 16,
        SeBackupPrivilege = 17,
        SeRestorePrivilege = 18,
        SeShutdownPrivilege = 19,
        SeDebugPrivilege = 20,
        SeAuditPrivilege = 21,
        SeSystemEnvironmentPrivilege = 22,
        SeChangeNotifyPrivilege = 23,
        SeRemoteShutdownPrivilege = 24,
        SeUndockPrivilege = 25,
        SeSyncAgentPrivilege = 26,
        SeEnableDelegationPrivilege = 27,
        SeManageVolumePrivilege = 28,
        SeImpersonatePrivilege = 29,
        SeCreateGlobalPrivilege = 30,
        SeTrustedCredManAccessPrivilege = 31,
        SeRelabelPrivilege = 32,
        SeIncreaseWorkingSetPrivilege = 33,
        SeTimeZonePrivilege = 34,
        SeCreateSymbolicLinkPrivilege = 35
    }
```
