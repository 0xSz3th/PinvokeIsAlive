
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool SystemTimeToFileTime([In] IntPtr lpSystemTime,
   IntPtr lpFileTime);
```

## Sample Code:
```cs
//malloc the SystemTime structure
    int stLen = Marshal.SizeOf(st);
    IntPtr pSystemTime = Marshal.AllocHGlobal(stLen);
    // copy SystemTime structure to the global heap
    Marshal.StructureToPtr(st, pSystemTime, true);

    //now malloc the Filetime;
    long lFileTime = 0;
    int ftLen = sizeof(long);
    IntPtr pFileTime = Marshal.AllocHGlobal(ftLen);

    //call the kernal32.dll SystemTimToFileTime method
    SystemTimeToFileTime(pSystemTime, pFileTime);

    //marshal the Filetime back into managed memory
    lFileTime = Marshal.ReadInt64(pFileTime);

    // convvert filetime to System.DateTime class
    DateTime dt = DateTime.FromFileTimeUtc(lFileTime);

    //free up resources
    Marshal.FreeHGlobal(pSystemTime);
    Marshal.FreeHGlobal(pFileTime);

    return dt;
```
