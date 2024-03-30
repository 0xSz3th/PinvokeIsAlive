
## C# Signature:
```cs
[DllImport("Wlanapi.dll",SetLastError=true)]
public static extern uint WlanScan(IntPtr hClientHandle,ref Guid pInterfaceGuid,IntPtr pDot11Ssid,IntPtr pIeData,IntPtr pReserved);
```

## VB Signature:
```cs
<DllImport("Wlanapi.dll", SetLastError:=True)>
Public Shared Function WlanScan(ByVal hClientHandle As IntPtr, ByRef pInterfaceGuid As Guid, ByVal pDot11Ssid As IntPtr, ByVal pIeData As IntPtr, ByVal pReserved As IntPtr) As UInteger
End Function
```

## Sample Code:
```cs
Guid g;
      //wlanHndl is the handle returned previously by calling [WlanOpenHandle]
      for (int i = 0; i < infoList.dwNumberOfItems; i++)
      {
      g = infoList.InterfaceInfo[i].InterfaceGuid;
      uint resultCode = WlanScan(wlanHndl, ref g, IntPtr.Zero, IntPtr.Zero, IntPtr.Zero);
      if (resultCode != 0)
          return;
      }
```
