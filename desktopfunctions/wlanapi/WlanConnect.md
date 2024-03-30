
## C# Signature:
```cs
[DllImport("Wlanapi.dll", SetLastError = true)]
public static extern uint WlanConnect(IntPtr hClientHandle,ref Guid pInterfaceGuid,ref WLAN_CONNECTION_PARAMETERS pConnectionParameters,IntPtr pReserved);
```

## VB Signature:
```cs
Declare Function WlanConnect Lib "wlanapi.dll" (ByVal hClientHandle As IntPtr, _
                         ByRef pInterfaceGuid As Guid, _
                         ByRef pConnectionParameters As WLAN_CONNECTION_PARAMETERS, _
                         ByVal pReserved As IntPtr) As UInteger
```

## Sample Code:
```cs
C#:

WLAN_CONNECTION_PARAMETERS wlanConnectionParameters = new WLAN_CONNECTION_PARAMETERS();
wlanConnectionParameters.dot11BssType = DOT11_BSS_TYPE.dot11_BSS_type_any;
wlanConnectionParameters.dwFlags = 0;
wlanConnectionParameters.strProfile = "dlink";
wlanConnectionParameters.wlanConnectionMode = WLAN_CONNECTION_MODE.wlan_connection_mode_profile;
WlanConnect(ClientHandle,ref pInterfaceGuid,ref wlanConnectionParameters ,new IntPtr());

VB:

Dim wlanConnectionParameters As New WLAN_CONNECTION_PARAMETERS
wlanConnectionParameters.dot11BssType = DOT11_BSS_TYPE.dot11_BSS_type_any
wlanConnectionParameters.dwFlags = 0
wlanConnectionParameters.strProfile = "dlink"
wlanConnectionParameters.wlanConnectionMode = WLAN_CONNECTION_MODE.wlan_connection_mode_profile
WlanConnect(ClientHandle, pInterfaceGuid, wlanConnectionParameters, IntPtr.Zero)
```
