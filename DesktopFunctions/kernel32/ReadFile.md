
## C# Signature:
```cs
//1
[DllImport("kernel32.dll", SetLastError = true)]
static extern bool ReadFile(IntPtr hFile, [Out] byte[] lpBuffer,
   uint nNumberOfBytesToRead, out uint lpNumberOfBytesRead, IntPtr lpOverlapped);
```

## C# Signature:
```cs
//2
[DllImport("kernel32.dll", SetLastError=true)]
static extern unsafe int ReadFile(IntPtr handle, IntPtr bytes, uint numBytesToRead, 
  IntPtr numBytesRead, NativeOverlapped* overlapped);
```

## C# Signature:
```cs
//3
[DllImport("kernel32.dll", SetLastError=true)]
static extern bool ReadFile(IntPtr hFile, [Out] byte[] lpBuffer, uint nNumberOfBytesToRead, 
   out uint lpNumberOfBytesRead, [In] ref System.Threading.NativeOverlapped lpOverlapped);
```

## C# Signature:
```cs
//4
[DllImport(@"kernel32.dll", SetLastError = true)]
static extern unsafe bool ReadFile(
    SafeFileHandle hFile,      // handle to file
    byte* pBuffer,        // data buffer, should be fixed
    int NumberOfBytesToRead,  // number of bytes to read
    IntPtr pNumberOfBytesRead,  // number of bytes read, provide IntPtr.Zero here
    NativeOverlapped *lpOverlapped // should be fixed, if not IntPtr.Zero
);
```

## VB Signature:
```cs
<DllImport("kernel32.dll", SetlastError:=True)> _
  Private Shared Function ReadFile(ByVal hFile As IntPtr, ByVal Buffer As IntPtr, _
    ByVal nNumberOfBytesToRead As Integer, ByRef lpNumberOfBytesRead As Integer, _
    ByRef lpOverlapped As OVERLAPPED) As Integer
  End Function
```

## VB Signature:
```cs
<DllImport("kernel32.dll")> Friend Shared Function ReadFile( _
    ByVal File As SafeFileHandle, _
    ByVal Buffer As System.Text.StringBuilder, _
    ByVal NumberOfBytesToRead As Integer, _
    ByRef NumberOfBytesRead As Integer, _
    ByRef Overlapped As System.Threading.NativeOverlapped) As SafeFileHandle
End Function
```

## Sample Code:
```cs
Public Function Read() As stArcnetPacket
    Dim dwErrorCode As FarcConstants
    Dim erg As stArcnetPacket
    Dim dwBytesReceived As Int32
    Dim ip As IntPtr = Marshal.AllocHGlobal(Marshal.SizeOf(erg))
    If ReadFile(hDriver, ip, Marshal.SizeOf(erg), dwBytesReceived, Nothing) Then
      erg = Marshal.PtrToStructure(ip, erg.GetType)
      ReDim Preserve erg.Data(dwBytesReceived - 6)
      Marshal.FreeHGlobal(ip)
    Else
      dwErrorCode = Marshal.GetLastWin32Error
      Marshal.FreeHGlobal(ip)
      Throw New System.IO.IOException("Read fails. Errorcode: " & _
    dwErrorCode.ToString, New System.ComponentModel.Win32Exception(dwErrorCode))
    End If
    Return erg
  End Function
```

## Sample Code:
```cs
// This is taken from the USBSharp.cs class
        public unsafe byte[] CT_ReadFile(int InputReportByteLength)
        {
            int BytesRead =0;
            byte[] BufBytes = new byte[InputReportByteLength];
            if (ReadFile(HidHandle, BufBytes, InputReportByteLength, ref BytesRead, null))
            {
                byte[] OutBytes = new byte[BytesRead];
                Array.Copy(BufBytes, OutBytes, BytesRead);
                return OutBytes;
            }
            else
            {
                return null;
            }
        }
```
