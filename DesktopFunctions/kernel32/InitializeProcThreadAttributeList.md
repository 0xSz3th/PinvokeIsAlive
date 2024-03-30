
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true)]
[return: MarshalAs(UnmanagedType.Bool)]
public static extern bool InitializeProcThreadAttributeList(
     IntPtr lpAttributeList,
     int dwAttributeCount,
     int dwFlags,
     ref IntPtr lpSize);
```

## Boo Signature:
```cs
[DllImport("kernel32.dll", SetLastError : true)]
def InitializeProcThreadAttributeList(
    lpAttributeList as IntPtr,
    dwAttributeCount as Int32,
    dwFlags as Int32,
    ref lpSize as IntPtr) as bool:
     pass
```

## Sample Code:
```cs
...
    if (attributeCount > 0)
    {
        flags = flags | EXTENDED_STARTUPINFO_PRESENT;
        startupInfoEx.lpAttributeList = InitializeProcThreadAttributeList(attributeCount);
    }
    ...
```

## Sample Code:
```cs
private static IntPtr InitializeProcThreadAttributeList(int attributeCount)
    {
        const int reserved = 0;
        var size = IntPtr.Zero;
        bool wasInitialized = InitializeProcThreadAttributeList(IntPtr.Zero, attributeCount, reserved, ref size);
        if (wasInitialized || size == IntPtr.Zero)
        {
        throw new Exception(string.Format("Couldn't get the size of the attribute list for {0} attributes", attributeCount));
        }

        IntPtr lpAttributeList = Marshal.AllocHGlobal(size);
        if (lpAttributeList == IntPtr.Zero)
        {
        throw new Exception("Couldn't reserve space for a new attribute list");
        }

        wasInitialized = InitializeProcThreadAttributeList(lpAttributeList, attributeCount, reserved, ref size);
        if (!wasInitialized)
        {
        throw new Exception("Couldn't create new attribute list");
        }

        return lpAttributeList;
    }
```
