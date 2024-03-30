
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true, CharSet = CharSet.Auto)]
static extern IntPtr OpenFileMapping(uint dwDesiredAccess, bool bInheritHandle,
   string lpName);
```

## Sample Code:
```cs
const UInt32 STANDARD_RIGHTS_REQUIRED = 0x000F0000;
        const UInt32 SECTION_QUERY = 0x0001;
        const UInt32 SECTION_MAP_WRITE = 0x0002;
        const UInt32 SECTION_MAP_READ = 0x0004;
        const UInt32 SECTION_MAP_EXECUTE = 0x0008;
        const UInt32 SECTION_EXTEND_SIZE = 0x0010;
        const UInt32 SECTION_ALL_ACCESS = (STANDARD_RIGHTS_REQUIRED|SECTION_QUERY|
            SECTION_MAP_WRITE |      
            SECTION_MAP_READ |       
            SECTION_MAP_EXECUTE |    
            SECTION_EXTEND_SIZE);
        const UInt32 FILE_MAP_ALL_ACCESS = SECTION_ALL_ACCESS;
        private IntPtr hHandle;
        private IntPtr pBuffer;
        unsafe public void Attach(string SharedMemoryName, UInt32 NumBytes)
        {
            if (IntPtr.Zero != hHandle) return;
            hHandle = OpenFileMapping(FILE_MAP_ALL_ACCESS, false, SharedMemoryName);
            if (IntPtr.Zero == hHandle) return;
            pBuffer = MapViewOfFile(hHandle, FILE_MAP_ALL_ACCESS, 0, 0, &NumBytes);
        }
        public void Detach()
        {
            if (IntPtr.Zero != hHandle)
            { 
                CloseHandle(hHandle); //fair to leak if can't close
                hHandle = IntPtr.Zero;
            }
            pBuffer = IntPtr.Zero;
            lBufferSize = 0;
        }
```
