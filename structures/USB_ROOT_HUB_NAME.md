
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
struct USB_ROOT_HUB_NAME
{
   public int ActualLength;
   [MarshalAs(UnmanagedType.ByValTStr, SizeConst = BUFFER_SIZE)]
   public string RootHubName;
}
```

## VB Definition:
```cs
Structure USB_ROOT_HUB_NAME 
   Public TODO
End Structure
```

## Notes:
```cs
typedef struct _USB_ROOT_HUB_NAME {
   ULONG  ActualLength;
   WCHAR  RootHubName[1];
} USB_ROOT_HUB_NAME, *PUSB_ROOT_HUB_NAME;
```

## Example:
```cs
// Open a handle to the Host Controller
IntPtr h = CreateFile(ControllerDevicePath, GENERIC_WRITE, FILE_SHARE_WRITE, IntPtr.Zero, OPEN_EXISTING, 0, IntPtr.Zero);
if (h.ToInt32() != INVALID_HANDLE_VALUE) 
{
   int nBytesReturned;
   USB_ROOT_HUB_NAME HubName = new USB_ROOT_HUB_NAME();
   int nBytes = Marshal.SizeOf(HubName);
   IntPtr ptrHubName = Marshal.AllocHGlobal(nBytes);

   // get the Hub Name
   if (DeviceIoControl(h, IOCTL_USB_GET_ROOT_HUB_NAME, ptrHubName, nBytes, ptrHubName, nBytes, out nBytesReturned, IntPtr.Zero))
   {
     HubName = (USB_ROOT_HUB_NAME)Marshal.PtrToStructure(ptrHubName, typeof(USB_ROOT_HUB_NAME));
     string HubDevicePath = @"\\.\" + HubName.RootHubName;
   }
   Marshal.FreeHGlobal(ptrHubName);
   CloseHandle(h);
}
Used with DeviceIoControl and [USB_ROOT_HUB_NAME] to get the Device Path to the USB Root Hub on a USB Controller5/15/2017 4:53:53 AM - -94.229.131.27
```
