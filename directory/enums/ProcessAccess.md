
## C# Definition:
```cs
[Flags]
public enum ProcessAccess
{
    /// <summary>
    /// Required to create a thread.
    /// </summary>
    CreateThread = 0x0002,

    /// <summary>
    /// 
    /// </summary>
    SetSessionId = 0x0004,

    /// <summary>
    /// Required to perform an operation on the address space of a process 
    /// </summary>
    VmOperation = 0x0008,

    /// <summary>
    /// Required to read memory in a process using ReadProcessMemory.
    /// </summary>
    VmRead = 0x0010,

    /// <summary>
    /// Required to write to memory in a process using WriteProcessMemory.
    /// </summary>
    VmWrite = 0x0020,

    /// <summary>
    /// Required to duplicate a handle using DuplicateHandle.
    /// </summary>
    DupHandle = 0x0040,

    /// <summary>
    /// Required to create a process.
    /// </summary>
    CreateProcess = 0x0080,

    /// <summary>
    /// Required to set memory limits using SetProcessWorkingSetSize.
    /// </summary>
    SetQuota = 0x0100,

    /// <summary>
    /// Required to set certain information about a process, such as its priority class (see SetPriorityClass).
    /// </summary>
    SetInformation = 0x0200,

    /// <summary>
    /// Required to retrieve certain information about a process, such as its token, exit code, and priority class (see OpenProcessToken).
    /// </summary>
    QueryInformation = 0x0400,

    /// <summary>
    /// Required to suspend or resume a process.
    /// </summary>
    SuspendResume = 0x0800,

    /// <summary>
    /// Required to retrieve certain information about a process (see GetExitCodeProcess, GetPriorityClass, IsProcessInJob, QueryFullProcessImageName). 
    /// A handle that has the PROCESS_QUERY_INFORMATION access right is automatically granted PROCESS_QUERY_LIMITED_INFORMATION.
    /// </summary>
    QueryLimitedInformation = 0x1000,

    /// <summary>
    /// Required to wait for the process to terminate using the wait functions.
    /// </summary>
    Synchronize = 0x100000,

    /// <summary>
    /// Required to delete the object.
    /// </summary>
    Delete = 0x00010000,

    /// <summary>
    /// Required to read information in the security descriptor for the object, not including the information in the SACL. 
    /// To read or write the SACL, you must request the ACCESS_SYSTEM_SECURITY access right. For more information, see SACL Access Right.
    /// </summary>
    ReadControl = 0x00020000,

    /// <summary>
    /// Required to modify the DACL in the security descriptor for the object.
    /// </summary>
    WriteDac = 0x00040000,

    /// <summary>
    /// Required to change the owner in the security descriptor for the object.
    /// </summary>
    WriteOwner = 0x00080000,

    StandardRightsRequired = 0x000F0000,

    /// <summary>
    /// All possible access rights for a process object.
    /// </summary>
    AllAccess = StandardRightsRequired | Synchronize | 0xFFFF
}
```

## VB.NET Definition:
```cs
<Flags()> _
Public Enum ProcessAccess As Integer
    ''' <summary>Specifies all possible access flags for the process object.</summary>
    AllAccess = CreateThread Or DuplicateHandle Or QueryInformation Or SetInformation Or Terminate Or VMOperation Or VMRead Or VMWrite Or Synchronize
    ''' <summary>Enables usage of the process handle in the CreateRemoteThread function to create a thread in the process.</summary>
    CreateThread = &H2
    ''' <summary>Enables usage of the process handle as either the source or target process in the DuplicateHandle function to duplicate a handle.</summary>
    DuplicateHandle = &H40
    ''' <summary>Enables usage of the process handle in the GetExitCodeProcess and GetPriorityClass functions to read information from the process object.</summary>
    QueryInformation = &H400
    ''' <summary>Enables usage of the process handle in the SetPriorityClass function to set the priority class of the process.</summary>
    SetInformation = &H200
    ''' <summary>Enables usage of the process handle in the TerminateProcess function to terminate the process.</summary>
    Terminate = &H1
    ''' <summary>Enables usage of the process handle in the VirtualProtectEx and WriteProcessMemory functions to modify the virtual memory of the process.</summary>
    VMOperation = &H8
    ''' <summary>Enables usage of the process handle in the ReadProcessMemory function to' read from the virtual memory of the process.</summary>
    VMRead = &H10
    ''' <summary>Enables usage of the process handle in the WriteProcessMemory function to write to the virtual memory of the process.</summary>
    VMWrite = &H20
    ''' <summary>Enables usage of the process handle in any of the wait functions to wait for the process to terminate.</summary>
    Synchronize = &H100000
End Enum
```

## Boo Definition:
```cs
[Flags]
enum ProcessAccess:
     All = 0x001F0FFF
     """Specifies all possible access flags for the process object."""
     CreateThread = 0x00000002
     """Enables usage of the process handle in the CreateRemoteThread function to create a thread in the process."""
     DuplicateHandle = 0x00000040
     """Enables usage of the process handle as either the source or target process in the DuplicateHandle function to duplicate a handle."""
     QueryInformation = 0x00000400
     """Enables usage of the process handle in the GetExitCodeProcess and GetPriorityClass functions to read information from the process object."""
     SetInformation = 0x00000200
     """Enables usage of the process handle in the SetPriorityClass function to set the priority class of the process."""
     Terminate = 0x00000001
     """Enables usage of the process handle in the TerminateProcess function to terminate the process."""
     VMOperation = 0x00000008
     """Enables usage of the process handle in the VirtualProtectEx and WriteProcessMemory functions to modify the virtual memory of the process."""
     VMRead = 0x00000010
     """Enables usage of the process handle in the ReadProcessMemory function to' read from the virtual memory of the process."""
     VMWrite = 0x00000020
     """Enables usage of the process handle in the WriteProcessMemory function to write to the virtual memory of the process."""
     Synchronize = 0x00100000
     """Enables usage of the process handle in any of the wait functions to wait for the process to terminate."""
```
