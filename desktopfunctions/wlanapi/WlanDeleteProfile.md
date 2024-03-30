
## C# Signature:
```cs
[DllImport("Wlanapi.dll", SetLastError = true, CharSet = CharSet.Unicode)]
public static extern uint WlanDeleteProfile(IntPtr hClientHandle,ref Guid pInterfaceGuid,string strProfileName,IntPtr pReserved);
```

## VB Signature:
```cs
Declare Function WlanDeleteProfile Lib "wlanapi.dll" (TODO) As TODO
```
