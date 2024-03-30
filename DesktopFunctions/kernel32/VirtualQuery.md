
## C# Signature:
```cs
[DllImport("kernel32.dll")]
private static extern int VirtualQuery (
    ref UIntPtr lpAddress, 
    ref MEMORY_BASIC_INFORMATION lpBuffer,
    int dwLength
);
```

## Sample Code:
```cs
[STAThread]
    static void Main(string[] args)
    {
        Memory memory = new Memory();
        memory.ShowMemory();

        Console.Read();
    }
```

## Sample Code:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct SYSTEM_INFO {
        internal PROCESSOR_INFO_UNION p;
        public uint dwPageSize;
        public IntPtr lpMinimumApplicationAddress;
        public IntPtr lpMaximumApplicationAddress;
        public UIntPtr dwActiveProcessorMask;
        public uint dwNumberOfProcessors;
        public uint dwProcessorType;
        public uint dwAllocationGranularity;
        public ushort wProcessorLevel;
        public ushort wProcessorRevision;
    };

    [StructLayout(LayoutKind.Explicit)]
    public struct PROCESSOR_INFO_UNION
    {
        [FieldOffset(0)]internal uint dwOemId;
        [FieldOffset(0)]internal ushort wProcessorArchitecture;
        [FieldOffset(2)]internal ushort wReserved;
    }

    [StructLayout(LayoutKind.Sequential)]
    public struct MEMORY_BASIC_INFORMATION 
    {
        public UIntPtr BaseAddress;
        public UIntPtr AllocationBase;
        public uint AllocationProtect;
        public IntPtr RegionSize;
        public uint State;
        public uint Protect;
        public uint Type;
    }

    SYSTEM_INFO system_info;
    MEMORY_BASIC_INFORMATION mbi;

    [DllImport("kernel32.dll")]
    private static extern int VirtualQuery (ref uint lpAddress, 
        ref MEMORY_BASIC_INFORMATION lpBuffer,
        int dwLength
    );

    [DllImport("kernel32.dll")]
    private static extern void GetSystemInfo(
        [MarshalAs(UnmanagedType.Struct)] ref SYSTEM_INFO lpSystemInfo
    );

    public Memory()
    {
        system_info = new SYSTEM_INFO();
        mbi = new MEMORY_BASIC_INFORMATION();
    }

    public void ShowMemory()
    {
        int iSize;

        GetSystemInfo(ref system_info);
        Console.WriteLine("dwProcessorType: {0}", system_info.dwProcessorType.ToString());
        Console.WriteLine("dwPageSize: {0}", system_info.dwPageSize.ToString());

        if (VirtualQuery(ref system_info.dwPageSize, 
            ref mbi, 
            (int)System.Runtime.InteropServices.Marshal.SizeOf(mbi)) != 0
        )
        {
            Console.WriteLine("AllocationBase: {0}", mbi.AllocationBase);
            Console.WriteLine("BaseAddress: {0}", mbi.BaseAddress);
            Console.WriteLine("RegionSize: {0}", mbi.RegionSize);
        }
        else
        {
            Console.WriteLine("ERROR: VirtualQuery() failed.");
        } 
    }
```
