
## C# Signature:
```cs
/// <summary>Retrieves the specified system information.</summary>
/// <param name="SystemInformationClass">indicate the kind of system information to be retrieved</param>
/// <param name="SystemInformation">a buffer that receives the requested information</param>
/// <param name="SystemInformationLength">The allocation size of the buffer pointed to by Info</param>
/// <param name="ReturnLength">If null, ignored.  Otherwise tells you the size of the information returned by the kernel.</param>
/// <returns>Status Information</returns>
[DllImport("ntdll.dll")]
public static extern NtStatus NtQuerySystemInformation(SYSTEM_INFORMATION_CLASS SystemInformationClass, IntPtr SystemInformation, uint SystemInformationLength, out uint ReturnLength);
```

## or:
```cs
[DllImport("ntdll.dll", PreserveSig = false)]
public static extern void NtQuerySystemInformation(SYSTEM_INFORMATION_CLASS SystemInformationClass, IntPtr SystemInformation, uint SystemInformationLength, out uint ReturnLength);
```

## VB Signature:
```cs
Declare Function NtQuerySystemInformation Lib "ntdll.dll" (TODO) As TODO
```

## Sample Code:
```cs
//helper method with "dynamic" buffer allocation 
public static IntPtr NtQuerySystemInformation(SYSTEM_INFORMATION_CLASS infoClass, uint infoLength = 0)
{
    if (infoLength == 0)
        infoLength = 0x10000;

    var infoPtr = Marshal.AllocHGlobal((int)infoLength);

    var tries = 0;
    while (true)
    {
        var result = NtQuerySystemInformation(infoClass, infoPtr, infoLength, out infoLength);

        if (result == NtStatus.Success)
             return infoPtr;

        Marshal.FreeHGlobal(infoPtr);  //free pointer when not Successful

        if (result != NtStatus.InfoLengthMismatch && result != NtStatus.BufferOverflow && result != NtStatus.BufferTooSmall)
        {
            //throw new Exception("Unhandled NtStatus " + result);
            return IntPtr.Zero;
        }

        if (++tries > 5)
            return IntPtr.Zero;

        infoPtr = Marshal.AllocHGlobal((int)infoLength);
    }
}
```

## Sample Code:
```cs
public void Test()
{  
    UInt32 
        result = 0;

    NativeMethods.SYSTEM_MEMORY_LIST_INFORMATION
        MemoryList;

    UInt32
        returnSize;

    Int32[]
        arr = new Int32[] { (Int32)Commands.MEMORYLIST };

    IntPtr
        buff = Marshal.AllocHGlobal(1024); // should be more than adequate
    try
    {
        result = (UInt32)NativeMethods.NtQuerySystemInformation(NativeMethods.SYSTEM_INFORMATION_CLASS.SystemMemoryListInformation, buff, result, out returnSize);
        if (result != 0)
            // Most likely error is InfoLengthMismatch = 0xc0000004 -- meaning you need to make the buffer larger
            throw new System.ComponentModel.Win32Exception(((NativeMethods.NtStatus)result).ToString());
        if (NativeMethods.SYSTEM_MEMORY_LIST_INFORMATION_SIZE == 0)
            NativeMethods.SYSTEM_MEMORY_LIST_INFORMATION_SIZE = returnSize; 
        MemoryList = (NativeMethods.SYSTEM_MEMORY_LIST_INFORMATION)Marshal.PtrToStructure(buff, typeof(NativeMethods.SYSTEM_MEMORY_LIST_INFORMATION));
    }
    finally
    {
        Marshal.FreeHGlobal(buff);
    }
}
```
