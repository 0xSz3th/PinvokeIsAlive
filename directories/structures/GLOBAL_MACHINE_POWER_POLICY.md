
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, Pack=1)]
struct GLOBAL_MACHINE_POWER_POLICY
{
   public uint Revision;
   public SYSTEM_POWER_STATE LidOpenWakeAc;
   public SYSTEM_POWER_STATE LidOpenWakeDc;
   public uint BroadcastCapacityResolution;
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential, Pack=1)>
Structure GLOBAL_MACHINE_POWER_POLICY 
   Public Revision As Integer
   Public LidOpenWakeAc As SYSTEM_POWER_STATE
   Public LidOpenWakeDc As SYSTEM_POWER_STATE
   Public BroadcastCapacityResolution As Integer
End Structure
```
