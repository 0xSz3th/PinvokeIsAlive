
## C# Signature:
```cs
[DllImport("ntdll.dll")]
public static extern NtStatus NtQueryObject(IntPtr objectHandle, OBJECT_INFORMATION_CLASS informationClass, IntPtr informationPtr, uint informationLength, ref uint returnLength);
```

## VB Signature:
```cs
Declare Function NtQueryObject Lib "ntdll.dll" (TODO) As TODO
```

## Sample Code:
```cs
//helper method with "dynamic" buffer allocation 
public static IntPtr NtQueryObject(IntPtr handle, OBJECT_INFORMATION_CLASS infoClass, uint infoLength = 0)
{
    if (infoLength == 0)
        infoLength = (uint)Marshal.SizeOf(typeof(uint));

    IntPtr infoPtr = Marshal.AllocHGlobal((int)infoLength);
    int tries = 0;
    NtStatus result;

    while (true)
    {
        result = NtQueryObject(handle, infoClass, infoPtr, infoLength, ref infoLength);

        if (result == NtStatus.InfoLengthMismatch || result == NtStatus.BufferOverflow || result == NtStatus.BufferTooSmall)
        {
            Marshal.FreeHGlobal(infoPtr);
            infoPtr = Marshal.AllocHGlobal((int)infoLength);
            tries++;
            continue;
        }
        else if (result == NtStatus.Success || tries > 5)
            break;
        else
        {
            //throw new Exception("Unhandled NtStatus " + result);
            break;
        }
    }

    if (result == NtStatus.Success)
        return infoPtr;//don't forget to free the pointer with Marshal.FreeHGlobal after you're done with it
    else
        Marshal.FreeHGlobal(infoPtr);//free pointer when not Successful

    return IntPtr.Zero;
}
```
