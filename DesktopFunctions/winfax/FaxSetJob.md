
## C# Signature:
```cs
[DllImport("winfax.dll")]
static extern bool FaxSetJob (IntPtr FaxHandle, int JobId,
   int Command, ref FAX_JOB_ENTRY JobEntry);
```

## VB Signature:
```cs
Declare Function FaxSetJob Lib "winfax.dll" (TODO) As TODO
```
