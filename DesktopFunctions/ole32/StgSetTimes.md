
## C# Signature:
```cs
[DllImport("ole32.dll")]
static extern int StgSetTimes([MarshalAs(UnmanagedType.LPWStr)] string
   lpszName, [In] ref FILETIME pctime, [In] ref FILETIME patime,
   [In] ref FILETIME pmtime);
```
