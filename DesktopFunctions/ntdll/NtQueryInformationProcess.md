
## C# Signature:
```cs
[DllImport("ntdll.dll", SetLastError=true)]
static extern int NtQueryInformationProcess(IntPtr processHandle, int processInformationClass, IntPtr processInformation, uint processInformationLength, IntPtr returnLength);
```

## or:
```cs
[DllImport("NTDLL.DLL", SetLastError=true)]
static extern int NtQueryInformationProcess(IntPtr hProcess, PROCESSINFOCLASS pic, out PROCESS_BASIC_INFORMATION pbi, int cb, out int pSize);
```

## or:
```cs
[DllImport("ntdll.dll", PreserveSig = false, SetLastError = true)]
public static extern void NtQueryInformationProcess(IntPtr ProcessHandle, PROCESSINFOCLASS ProcessInformationClass, out PROCESS_EXTENDED_BASIC_INFORMATION ProcessInformation, uint ProcessInformationLength, out uint ReturnLength);
```

## VB Signature:
```cs
Declare Function NtQueryInformationProcess Lib "ntdll.dll" ( _
   processHandle As IntPtr, processInformationClass As Integer, _
   processInformation As IntPtr, processInformationLength As Integer, _
   returnLength As IntPtr) As Integer
```

## Boo Signature:
```cs
[DllImport("ntdll.dll", SetLastError : true)]
def NtQueryInformationProcess(
     hProcess as IntPtr,
     processInformationClass as PROCESSINFOCLASS,
     ref processInformation as PROCESS_BASIC_INFORMATION,
     processInformationLength as UInt32,
     ref returnLength as UInt32) as UInt32:
     pass
```

## User-Defined Types:
```cs
[PROCESSINFOCLASS], [PROCESS_BASIC_INFORMATION], [PROCESS_EXTENDED_BASIC_INFORMATION]
// deleted a lot of unused entries
enum PROCESSINFOCLASS:
     ProcessBasicInformation = 0x00
     ProcessDebugPort = 0x07
     ProcessExceptionPort = 0x08
     ProcessAccessToken = 0x09
     ProcessWow64Information = 0x1A
     ProcessImageFileName = 0x1B
     ProcessDebugObjectHandle = 0x1E
     ProcessDebugFlags = 0x1F
     ProcessExecuteFlags = 0x22
     ProcessInstrumentationCallback = 0x28
     MaxProcessInfoClass = 0x64

[StructLayout(LayoutKind.Sequential)]
struct PROCESS_BASIC_INFORMATION:
     Reserved1 as IntPtr
     PebAddress as IntPtr
     [MarshalAs(UnmanagedType.ByValArray, SizeConst : 2)]
     Reserved2 as (IntPtr)
     UniquePid as IntPtr
     Reserved3 as IntPtr
```

## Sample Code:
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

## Or:
```cs
public static int GetParentProcessId()
    {
        PROCESS_BASIC_INFORMATION pbi = new PROCESS_BASIC_INFORMATION();

        //Get a handle to our own process
        IntPtr hProc = OpenProcess((ProcessAccessFlags)0x001F0FFF, false, Process.GetCurrentProcess().Id);

        try
        {
            int sizeInfoReturned;
            int queryStatus = NtQueryInformationProcess(hProc, (PROCESSINFOCLASS)0, ref pbi, pbi.Size, out sizeInfoReturned);
        }
        finally
        {
            if (!hProc.Equals(IntPtr.Zero))
            {
            //Close handle and free allocated memory
            CloseHandle(hProc);
            hProc = IntPtr.Zero;
            }
        }

        return (int)pbi.InheritedFromUniqueProcessId;
    }
```
