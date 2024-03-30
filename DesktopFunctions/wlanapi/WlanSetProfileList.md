
## C# Signature:
```cs
[DllImport("Wlanapi.dll",SetLastError = true,CharSet = CharSet.Unicode)]
public static extern uint WlanSetProfileList(IntPtr hClientHandle,ref Guid pInterfaceGuid,uint dwItems,string[] strProfileNames,IntPtr pReserved);
```

## VB Signature:
```cs
Declare Function WlanSetProfileList Lib "wlanapi.dll" (TODO) As TODO
```
