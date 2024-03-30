```cs
public static IntPtr GetPEBAddress()
    {
        //Get a handle to our own process
        IntPtr hProc = OpenProcess(0x001F0FFF, false, Process.GetCurrentProcess().Id);
        //Allocate memory for a new PROCESS_BASIC_INFORMATION structure
        IntPtr pbi = Marshal.AllocHGlobal(Marshal.SizeOf(typeof(PROCESS_BASIC_INFORMATION)));
        //Allocate memory for a long
        IntPtr outLong = Marshal.AllocHGlobal(sizeof(long));
        IntPtr outPtr = IntPtr.Zero;

        int queryStatus = false;

        //Store API call success in a boolean
        queryStatus = NtQueryInformationProcess(hProc, 0, pbi, (uint)Marshal.SizeOf(typeof(PROCESS_BASIC_INFORMATION)), outLong);

        //Close handle and free allocated memory
        CloseHandle(hProc);
        Marshal.FreeHGlobal(outLong);

        //STATUS_SUCCESS = 0, so if API call was successful querySuccess should contain 0 ergo we reverse the check.
        if(!queryStatus )
        outPtr = PtrToStructure<PROCESS_BASIC_INFORMATION>(pbi, typeof(PROCESS_BASIC_INFORMATION)).PebBaseAddress;

        //Free allocated space
        Marshal.FreeHGlobal(pbi);

        //Return pointer to PEB base address
        return outPtr;
    }
```