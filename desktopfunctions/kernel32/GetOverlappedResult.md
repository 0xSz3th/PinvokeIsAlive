
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
static extern bool GetOverlappedResult(IntPtr hFile, 
   [In] ref System.Threading.NativeOverlapped lpOverlapped, 
   out uint lpNumberOfBytesTransferred, bool bWait);
```

## Sample Code:
```cs
public static bool WriteUSB(IntPtr hDevice, byte[] pBuffer, uint dwBytesToWrite, ref uint lpNumberOfBytesWritten)
    {
        NativeOverlapped lpOverlapped = new NativeOverlapped();

        if (!WriteFile(hDevice, pBuffer, dwBytesToWrite, ref lpNumberOfBytesWritten, ref lpOverlapped) &&
        Marshal.GetLastWin32Error() == ERROR_IO_PENDING)
        {
        return GetOverlappedResult(hDevice, ref lpOverlapped, ref lpNumberOfBytesWritten, true);
        }
        return false;
    }
```
