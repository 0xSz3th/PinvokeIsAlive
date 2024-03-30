
## C# Signature:
```cs
[DllImport("Netapi32.dll", SetLastError=true)]
static extern int NetApiBufferFree(IntPtr Buffer);
```

## VB .NET Signature:
```cs
Declare Unicode Function NetApiBufferFree Lib "netapi32.dll" _
    (ByVal buffer As IntPtr) As Long
```

## Notes:
```cs
Changed VB.NET Signature from "ByRef buffer" to "ByVal buffer". With ByRef you get a significant memory leak, with ByVal everything is fine.
```

## Notes:
```cs
Added VB definition & sample.
```

## Sample Code:
```cs
VB.NET:
' Edited down code to only show usage of NetApiBufferFree()
Dim BufPtr As IntPtr        'in
retval = NetShareEnum(SvrNameBldr, 2, BufPtr, MAX_PREFERRED_LENGTH, dwEntriesread, dwTotalentries, dwResumehandle)
Call NetApiBufferFree(BufPtr)
```
