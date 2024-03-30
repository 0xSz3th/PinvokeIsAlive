
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true)]
[return: MarshalAs(UnmanagedType.Bool)]
public static extern bool UpdateProcThreadAttribute(
     IntPtr lpAttributeList,
     uint dwFlags,
     IntPtr Attribute,
     IntPtr lpValue,
     IntPtr cbSize,
     IntPtr lpPreviousValue,
     IntPtr lpReturnSize);
```

## Boo Signature:
```cs
[DllImport("kernel32.dll", SetLastError : true)]
def UpdateProcThreadAttribute(
    lpAttributeList as IntPtr,
    dwFlags as UInt32,
    Attribute as IntPtr,
    lpValue as IntPtr,
    cbSize as IntPtr,
    lpPreviousValue as IntPtr,
    lpReturnSize as IntPtr) as bool:
     pass
```

## User-Defined Types:
```cs
(WinBase.h)
    ...
    PROC_THREAD_ATTRIBUTE_PARENT_PROCESS = 0x00020000,
    PROC_THREAD_ATTRIBUTE_HANDLE_LIST    = 0x00020002
    ...

    and [STARTUPINFOEX]
```

## Sample Code:
```cs
private static void SetNewProcessParent(ref STARTUPINFOEX startupInfoEx, int parentProcessId)
    {
        const int reserved = 0;
        var parentProcess = Process.GetProcessById(parentProcessId);
        IntPtr lpValue = Marshal.AllocHGlobal(IntPtr.Size);
        Marshal.WriteIntPtr(lpValue, parentProcess.Handle);

        bool success = UpdateProcThreadAttribute(
        startupInfoEx.lpAttributeList,
        reserved,
        PROC_THREAD_ATTRIBUTE_PARENT_PROCESS,
        lpValue,
        (IntPtr)IntPtr.Size,
        IntPtr.Zero,
        IntPtr.Zero);

        if (!success)
        {
        throw new Exception(string.Format("Error setting [{0}] as the parentPid for the new process", parentProcessId));
        }
    }

    private static void SetInheritableHandles(ref STARTUPINFOEX startupInfoEx, ICollection<IntPtr> inheritableHandles)
    {
        const int reserved = 0;
        var handleArray = inheritableHandles.ToArray();
        var pinnedHandleArray = GCHandle.Alloc(handleArray, GCHandleType.Pinned);
        IntPtr handles = pinnedHandleArray.AddrOfPinnedObject();

        bool success = UpdateProcThreadAttribute(
        startupInfoEx.lpAttributeList,
        reserved,
        PROC_THREAD_ATTRIBUTE_HANDLE_LIST,
        handles,
        (IntPtr)(inheritableHandles.Count * IntPtr.Size),
        IntPtr.Zero,
        IntPtr.Zero);

        if (!success)
        {
        throw new Exception("Error adding inheritable handles to process launch");
        }
    }
```
