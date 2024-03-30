
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
struct STORAGE_DEVICE_NUMBER
{
   public int DeviceType;
   public int DeviceNumber;
   public int PartitionNumber;
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _
Structure STORAGE_DEVICE_NUMBER
    Public DeviceType As Integer
    Public DeviceNumber As Integer
    Public PartitionNumber As Integer
End Structure
```

## Example:
```cs
public const uint OPEN_EXISTING = 3;
public const uint INVALID_HANDLE_VALUE = 0;
public const int IOCTL_STORAGE_GET_DEVICE_NUMBER = 0x2D1080;

[System.Runtime.InteropServices.DllImport("Kernel32.dll", SetLastError = true)]
public extern static IntPtr CreateFile(string FileName, uint DesiredAccess,
    uint ShareMode, IntPtr lpSecurityAttributes,
    uint CreationDisposition, uint dwFlagsAndAttributes,
    IntPtr hTemplateFile);

[System.Runtime.InteropServices.DllImport("Kernel32.dll", SetLastError = true)]
public extern static int CloseHandle(IntPtr hObject);

[System.Runtime.InteropServices.DllImport("Kernel32.dll", SetLastError = true)]
public extern static bool DeviceIoControl(IntPtr hDevice, uint IoControlCode,
    IntPtr InMediaRemoval, uint InBufferSize,
    IntPtr OutBuffer, int OutBufferSize,
    out int BytesReturned,
    IntPtr Overlapped);

// return a unique device number for the given device path
int GetDeviceNumber(string DevicePath)
{
   int ans = -1;

   IntPtr h = CreateFile(DevicePath.TrimEnd('\\'), 0, 0, IntPtr.Zero, OPEN_EXISTING, 0, IntPtr.Zero);
   if (h.ToInt32() != INVALID_HANDLE_VALUE)
   {
     int requiredSize;
     STORAGE_DEVICE_NUMBER Sdn = new STORAGE_DEVICE_NUMBER();
     int nBytes = Marshal.SizeOf(Sdn);
     IntPtr ptrSdn = Marshal.AllocHGlobal(nBytes);

     if (DeviceIoControl(h, IOCTL_STORAGE_GET_DEVICE_NUMBER, IntPtr.Zero, 0, ptrSdn, nBytes, out requiredSize, IntPtr.Zero))
     {
       Sdn = (STORAGE_DEVICE_NUMBER)Marshal.PtrToStructure(ptrSdn, typeof(STORAGE_DEVICE_NUMBER));
       // just my way of combining the relevant parts of the
       // STORAGE_DEVICE_NUMBER into a single number
       ans = (Sdn.DeviceType << 8) + Sdn.DeviceNumber;
     }
     Marshal.FreeHGlobal(ptrSdn);
     CloseHandle(h);
   }
   return ans;
}
```
