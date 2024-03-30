
## C# Signature:
```cs
[StructLayout(LayoutKind.Sequential)]
    struct TCITEM
    {
        public uint mask;
        public int state;
        public int statemask;
        public IntPtr text;
        public int size;
        public int image;
        public int param;
    }
```

## VB Signature:
```cs
Declare Function TCITEM Lib "user32.dll" (TODO) As TODO
```

## Sample Code:
```cs
#region code
    TCITEM tcitem = new TCITEM();
    tcitem.size = 200;
    uint ProcessID;
    GetWindowThreadProcessId((IntPtr)handle, out ProcessID);
    IntPtr process = OpenProcess(ProcessAccessFlags.VMOperation | ProcessAccessFlags.VMRead |
    ProcessAccessFlags.VMWrite | ProcessAccessFlags.QueryInformation, false, ProcessID);

    IntPtr pszTextPtr = VirtualAllocEx(process, IntPtr.Zero, 512, AllocationType.Commit, MemoryProtection.ReadWrite);
    IntPtr tcitemPtr = VirtualAllocEx(process, IntPtr.Zero, (uint)Marshal.SizeOf(typeof(TCITEM)), AllocationType.Commit, MemoryProtection.ReadWrite);

    const int TCIF_STATE = 0x10;
    const int TCIF_TEXT = 0x1;
    tcitem.mask = TCIF_STATE | TCIF_TEXT;

    tcitem.text = pszTextPtr;
    string L_buf = "nasenmann ";
    IntPtr TextPtr = Marshal.StringToHGlobalAnsi(L_buf);
    L_buf = "überschrieben";
    int bytesReaded;
    WriteProcessMemory(process, pszTextPtr, TextPtr, 512, IntPtr.Zero);
    Marshal.FreeHGlobal(TextPtr);
    IntPtr ptr = Marshal.AllocHGlobal(Marshal.SizeOf(tcitem));
    Marshal.StructureToPtr(tcitem, ptr, true);
    tcitem.size = 1; // überschrieben
    WriteProcessMemory(process, tcitemPtr, ptr, Marshal.SizeOf(tcitem), IntPtr.Zero);
    Marshal.FreeHGlobal(ptr);
    int res = SendMessage(handle, TCM_GETITEMA, index, tcitemPtr);
    ptr = Marshal.AllocHGlobal(512);
    ReadProcessMemory(process, pszTextPtr, ptr, 512, out bytesReaded);
    L_buf = Marshal.PtrToStringAnsi(ptr);
    Marshal.FreeHGlobal(ptr);
    ptr = Marshal.AllocHGlobal(Marshal.SizeOf(tcitem));
    ReadProcessMemory(process, tcitemPtr, ptr, (int)Marshal.SizeOf(tcitem), out bytesReaded);
    tcitem = (TCITEM)Marshal.PtrToStructure(ptr, tcitem.GetType());
    Marshal.FreeHGlobal(ptr);
    VirtualFreeEx(process, tcitemPtr, 0, FreeType.Release);
    VirtualFreeEx(process, pszTextPtr, 0, FreeType.Release);

    #endregion

    #region defines
    [Flags]
    public enum FreeType
    {
    Decommit = 0x4000,
    Release = 0x8000,
    }

    [Flags]
    enum ProcessAccessFlags : uint
    {
    All = 0x001F0FFF,
    Terminate = 0x00000001,
    CreateThread = 0x00000002,
    VMOperation = 0x00000008,
    VMRead = 0x00000010,
    VMWrite = 0x00000020,
    DupHandle = 0x00000040,
    SetInformation = 0x00000200,
    QueryInformation = 0x00000400,
    Synchronize = 0x00100000
    }

    [Flags]
    public enum AllocationType
    {
    Commit = 0x1000,
    Reserve = 0x2000,
    Decommit = 0x4000,
    Release = 0x8000,
    Reset = 0x80000,
    Physical = 0x400000,
    TopDown = 0x100000,
    WriteWatch = 0x200000,
    LargePages = 0x20000000
    }

    [Flags]
    public enum MemoryProtection
    {
    Execute = 0x10,
    ExecuteRead = 0x20,
    ExecuteReadWrite = 0x40,
    ExecuteWriteCopy = 0x80,
    NoAccess = 0x01,
    ReadOnly = 0x02,
    ReadWrite = 0x04,
    WriteCopy = 0x08,
    GuardModifierflag = 0x100,
    NoCacheModifierflag = 0x200,
    WriteCombineModifierflag = 0x400
    }

    [DllImport("user32.dll", SetLastError = true)]
    static extern uint GetWindowThreadProcessId(IntPtr hWnd, out uint lpdwProcessId);
    [DllImport("kernel32.dll", SetLastError = true, ExactSpelling = true)]
    static extern IntPtr VirtualAllocEx(IntPtr hProcess, IntPtr lpAddress,
       uint dwSize, AllocationType flAllocationType, MemoryProtection flProtect);
    [DllImport("kernel32.dll")]
    static extern IntPtr OpenProcess(ProcessAccessFlags dwDesiredAccess, [MarshalAs(UnmanagedType.Bool)] bool bInheritHandle, uint dwProcessId);
    [DllImport("kernel32.dll", SetLastError = true, ExactSpelling = true)]
    static extern bool VirtualFreeEx(IntPtr hProcess, IntPtr lpAddress,
       int dwSize, FreeType dwFreeType);
    [DllImport("kernel32.dll", SetLastError = true)]
    static extern bool ReadProcessMemory(
     IntPtr hProcess,
     IntPtr lpBaseAddress,
    IntPtr lpBuffer,
     int dwSize,
     out int lpNumberOfBytesRead
    );
    [DllImport("kernel32.dll", SetLastError = true)]
    static extern bool WriteProcessMemory(IntPtr hProcess, IntPtr lpBaseAddress, IntPtr lpBuffer, int nSize, IntPtr lpNumberOfBytesWritten);
    #endregion
```
