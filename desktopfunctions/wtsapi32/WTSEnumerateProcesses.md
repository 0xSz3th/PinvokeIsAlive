
## C# Signature:
```cs
[DllImport("wtsapi32.dll", SetLastError=true)]
static extern bool WTSEnumerateProcesses(
    IntPtr serverHandle, // Handle to a terminal server. 
    Int32  reserved,     // must be 0
    Int32  version,      // must be 1
    ref IntPtr ppProcessInfo, // pointer to array of WTS_PROCESS_INFO
    ref Int32  pCount     // pointer to number of processes
);
```

## VB Signature:
```cs
Private Declare Function WTSEnumerateProcesses Lib "wtsapi32.dll" ( _
     ByVal hServer As Int32, _
     ByVal Reserved As Int32, _
     ByVal Version As Int32, _
     ByRef ppProcessInfo As IntPtr, _
     ByRef pCount As Int32
) As Int32
```

## Sample Code:
```cs
//C# sample code

//Handle to the server that this code is running on.

[DllImport("wtsapi32.dll")]
private static extern void WTSFreeMemory(IntPtr pMemory);

private static HANDLE WTS_CURRENT_SERVER_HANDLE = (IntPtr)null;

public static WTS_PROCESS_INFO[] WTSEnumerateProcesses()
{
    IntPtr pProcessInfo = IntPtr.Zero;
    int processCount = 0;

    if (!WTSEnumerateProcesses(WTS_CURRENT_SERVER_HANDLE, 0, 1, ref pProcessInfo, ref processCount))
        return null;

    IntPtr pMemory = pProcessInfo;
    WTS_PROCESS_INFO[] processInfos = new WTS_PROCESS_INFO[processCount];
    for (int i = 0; i < processCount; i++)
    {
        processInfos[i] = (WTS_PROCESS_INFO)Marshal.PtrToStructure(pProcessInfo, typeof(WTS_PROCESS_INFO));
        pProcessInfo = (IntPtr)((long)pProcessInfo + Marshal.SizeOf(processInfos[i]));
    }

    WTSFreeMemory(pMemory);
    return processInfos;
}
```

## Sample Code:
```cs
//VB sample code
Dim strucProcessInfo As WTS_PROCESS_INFO
Dim ptrProcessInfo As IntPtr
Dim lngPtrPos As Long
Dim intReturn As Integer
Dim intCount As Integer
Dim intProcessCount As Integer
Dim strProcessName As String

intReturn = WTSEnumerateProcesses(WTS_CURRENT_SERVER_HANDLE, 0, 1, ptrProcessInfo, intProcessCount)
If intReturn > 0 Then
    'Get the length in bytes of each structure...
    lngPtrPos = ptrProcessInfo.ToInt32()

    For intCount = 0 To intProcessCount - 1
        strucProcessInfo = Marshal.PtrToStructure(New IntPtr(lngPtrPos), strucProcessInfo.GetType)
        'ProcessName is merely a pointer to the string - convert it to the full string...
        strProcessName = Marshal.PtrToStringAnsi(New IntPtr(strucProcessInfo.ProcessName))

        Console.WriteLine ("Process Name: " & strProcessName)
        Console.WriteLine ("Process ID: " & strucProcessInfo.ProcessID)
        Console.WriteLine ("Session ID: " & strucProcessInfo.SessionID)

        'Now move on the pointer to the next member of the array...
        lngPtrPos = lngPtrPos + Len(strucProcessInfo)
    Next
End If

Call WTSFreeMemory(ptrProcessInfo)
```
