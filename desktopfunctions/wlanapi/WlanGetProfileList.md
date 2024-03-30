
## C# Signature:
```cs
[DllImport("wlanapi.dll", SetLastError = true, CallingConvention=CallingConvention.Winapi)]
private static extern uint WlanGetProfileList(
    [In] IntPtr clientHandle,
    [In, MarshalAs(UnmanagedType.LPStruct)] Guid interfaceGuid,
    [In] IntPtr pReserved,
    [Out] out IntPtr profileList
);
```

## VB Signature:
```cs
Declare Function WlanGetProfileList Lib "wlanapi.dll" (TODO) As TODO
```

## Sample Code:
```cs
IntPtr ppProfileList;
WlanGetProfileList(ClientHandle, pInterfaceGuid, IntPtr.Zero, out ppProfileList);
WLAN_PROFILE_INFO_LIST wlanProfileInfoList = new WLAN_PROFILE_INFO_LIST(ppProfileList);
```
