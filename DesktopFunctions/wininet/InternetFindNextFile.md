
## C# Signature:
```cs
[DllImport("wininet.dll", SetLastError = true, CharSet = CharSet.Auto)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool InternetFindNextFile(IntPtr hFind,
   out WIN32_FIND_DATA findFileData);
```

## VB Signature:
```cs
Declare Function InternetFindNextFile Lib "wininet.dll" _
   (ByVal hFind As IntPtr, ByRef findFileData As WIN32_FIND_DATA) _
   As <MarshalAs(UnmanagedType.Bool)> Boolean
```
