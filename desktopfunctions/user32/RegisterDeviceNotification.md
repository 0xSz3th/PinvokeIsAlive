
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError = true)]
static extern IntPtr RegisterDeviceNotification(IntPtr hRecipient,
   IntPtr NotificationFilter, uint Flags);
```

## VB Signature:
```cs
<DllImport("user32.dll", CharSet:=CharSet.Auto, SetLastError:=true)> _
Function RegisterDeviceNotification(ByVal hRecipient As IntPtr, _
                            ByVal NotificationFilter As IntPtr, _
                            ByVal Flags As Int32) _
    As IntPtr 
End Function
```

## Sample Code:
```cs
Public Const DEVICE_NOTIFY_WINDOW_HANDLE As Integer = 0

deviceNotificationHandle=RegisterDeviceNotification(formHandle, DevBroadcastInterfaceBuffer, DEVICE_NOTIFY_WINDOW_HANDLE)
```
