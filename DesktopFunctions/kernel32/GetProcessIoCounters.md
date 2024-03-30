
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool GetProcessIoCounters(IntPtr hProcess,
   out IO_COUNTERS lpIoCounters);
```

## Sample Code:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
    static extern bool GetProcessIoCounters(IntPtr hProcess, out IO_COUNTERS lpIoCounters);

    [StructLayout(LayoutKind.Sequential)]
    struct IO_COUNTERS
    {
        public UInt64 ReadOperationCount;
        public UInt64 WriteOperationCount;
        public UInt64 OtherOperationCount;
        public UInt64 ReadTransferCount;
        public UInt64 WriteTransferCount;
        public UInt64 OtherTransferCount;
    };
    public IO_COUNTERS info;

    public void show_read_count()
    {
        if (GetProcessIoCounters(Process.GetCurrentProcess().Handle, out info) == false)
        {
            int error_code = Marshal.GetLastWin32Error();
            if (error_code != 0) Debug.WriteLine((new Win32Exception(error_code)).Message);
        }
        else
        {
            Debug.WriteLine(info.ReadOperationCount);
        }
    }
```
