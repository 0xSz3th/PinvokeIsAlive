
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, Pack=1)]
struct USB_NODE_CONNECTION_INFORMATION_EX
{
   public int ConnectionIndex;
   public USB_DEVICE_DESCRIPTOR DeviceDescriptor;
   public byte CurrentConfigurationValue;
   public byte Speed;
   public byte DeviceIsHub;
   public short DeviceAddress;
   public int NumberOfOpenPipes;
   public int ConnectionStatus;
   //public IntPtr PipeList;
}
```

## VB Definition:
```cs
Structure USB_NODE_CONNECTION_INFORMATION_EX 
   Public TODO
End Structure
```

## Notes:
```cs
typedef struct _USB_NODE_CONNECTION_INFORMATION_EX {
   ULONG  ConnectionIndex;
   USB_DEVICE_DESCRIPTOR  DeviceDescriptor;
   UCHAR  CurrentConfigurationValue;
   UCHAR  Speed;
   BOOLEAN  DeviceIsHub;
   USHORT  DeviceAddress;
   ULONG  NumberOfOpenPipes;
   USB_CONNECTION_STATUS  ConnectionStatus;
   USB_PIPE_INFO  PipeList[0];
} USB_NODE_CONNECTION_INFORMATION_EX, *PUSB_NODE_CONNECTION_INFORMATION_EX;
```

## Example:
```cs
// Open a handle to the Hub device
IntPtr h = CreateFile(HubDevicePath, GENERIC_WRITE, FILE_SHARE_WRITE, IntPtr.Zero, OPEN_EXISTING, 0, IntPtr.Zero);
if (h.ToInt32() != INVALID_HANDLE_VALUE)
{
   int nBytes = Marshal.SizeOf(typeof(USB_NODE_CONNECTION_INFORMATION_EX));
   IntPtr ptrNodeConnection = Marshal.AllocHGlobal(nBytes);

   // loop thru all of the ports on the hub
   // BTW: Ports are numbered starting at 1
   for (int i = 1; i <= HubPortCount; i++)
   {
     int nBytesReturned;
     USB_NODE_CONNECTION_INFORMATION_EX NodeConnection = new USB_NODE_CONNECTION_INFORMATION_EX();
     NodeConnection.ConnectionIndex = i;
     Marshal.StructureToPtr(NodeConnection, ptrNodeConnection, true);

     if (DeviceIoControl(h, IOCTL_USB_GET_NODE_CONNECTION_INFORMATION_EX, ptrNodeConnection, nBytes, ptrNodeConnection, nBytes, out nBytesReturned, IntPtr.Zero))
     {
       NodeConnection = (USB_NODE_CONNECTION_INFORMATION_EX)Marshal.PtrToStructure(ptrNodeConnection, typeof(USB_NODE_CONNECTION_INFORMATION_EX));
       // do something here...
     }
   }
   Marshal.FreeHGlobal(ptrNodeConnection);
   CloseHandle(h);
}
```

## Example:
```cs
// To get the USB_PIPE_INFO data
for (int i = 0; i < HubPortCount; i++)
{
   USB_NODE_CONNECTION_INFORMATION_EX connection = new USB_NODE_CONNECTION_INFORMATION_EX();
   connection.ConnectionIndex = i;
   size = Marshal.SizeOf(typeof(USB_NODE_CONNECTION_INFORMATION_EX)) + 32 * Marshal.SizeOf(typeof(USB_PIPE_INFO)); // Assuming 32 should be enough, you can make this larger

   IntPtr ptr_connection = Marshal.AllocHGlobal(size);
   Marshal.StructureToPtr(connection, ptr_connection, true);

   int bytes_returned;
   if (DeviceIoControl(hHub, IOCTL_USB_GET_NODE_CONNECTION_INFORMATION_EX, ptr_connection, size, ptr_connection, size, out bytes_returned, IntPtr.Zero))
   {
     connection = (USB_NODE_CONNECTION_INFORMATION_EX)Marshal.PtrToStructure(ptr_connection, typeof(USB_NODE_CONNECTION_INFORMATION_EX));

     if (bytes_returned != Marshal.SizeOf(typeof(USB_NODE_CONNECTION_INFORMATION_EX)))
     {
       IntPtr ptr_pipeinfo;

       int num = (bytes_returned - Marshal.SizeOf(typeof(USB_NODE_CONNECTION_INFORMATION_EX))) / Marshal.SizeOf(typeof(USB_PIPE_INFO));
       USB_PIPE_INFO[] pipe_info = new USB_PIPE_INFO[num];

       for (int j = 0; j < num; j++)
       {
     // Set ptr to an USB_PIPE_INFO element and marshal it back
     IntPtr ptr_pipeinfo = new IntPtr((byte*)ptr_connection.ToPointer() 
                       + Marshal.SizeOf(typeof(USB_NODE_CONNECTION_INFORMATION_EX)) 
                       + j * Marshal.SizeOf(typeof(USB_PIPE_INFO)));
     pipe_info[j] = (USB_PIPE_INFO)Marshal.PtrToStructure(ptr_pipeinfo, typeof(USB_PIPE_INFO));
       }
     }
   }

   Marshal.FreeHGlobal(ptr_connection);
}
Used with DeviceIoControl and [USB_NODE_CONNECTION_INFORMATION_EX] to get information from a port on a USB Hub5/15/2017 4:53:18 AM - -94.229.131.27
```
