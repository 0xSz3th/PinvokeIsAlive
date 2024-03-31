
## C# Definition:
```cs
enum USB_CONNECTION_STATUS
{
   NoDeviceConnected,
   DeviceConnected,
   DeviceFailedEnumeration,
   DeviceGeneralFailure,
   DeviceCausedOvercurrent,
   DeviceNotEnoughPower,
   DeviceNotEnoughBandwidth,
   DeviceHubNestedTooDeeply,
   DeviceInLegacyHub
}
```

## VB Definition:
```cs
Enum USB_CONNECTION_STATUS
   TODO
End Enum
```

## Notes:
```cs
typedef enum _USB_CONNECTION_STATUS {
   NoDeviceConnected,
   DeviceConnected,
   DeviceFailedEnumeration,
   DeviceGeneralFailure,
   DeviceCausedOvercurrent,
   DeviceNotEnoughPower,
   DeviceNotEnoughBandwidth,
   DeviceHubNestedTooDeeply,
   DeviceInLegacyHub
} USB_CONNECTION_STATUS, *PUSB_CONNECTION_STATUS;
```
