
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true, CharSet = CharSet.Unicode)]
    public static extern IntPtr FindFirstFileEx(
        string lpFileName,
        FINDEX_INFO_LEVELS fInfoLevelId,
        out WIN32_FIND_DATA lpFindFileData,
        FINDEX_SEARCH_OPS fSearchOp,
        IntPtr lpSearchFilter,
        int dwAdditionalFlags);
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll", CharSet:=CharSet.Auto)> _
    Private Function FindFirstFileEx(ByVal lpFileName As String, ByVal fInfoLevelId As FINDEX_INFO_LEVELS, ByRef lpFindFileData As WIN32_FIND_DATA, ByVal fSearchOp As FINDEX_SEARCH_OPS, lpSearchFilter As Int32, dwAdditionalFlags As Integer) As Int32
    End Function
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll", CharSet:=CharSet.Unicode)> _
    Public Shared Function FindFirstFileExW(ByVal lpFileName As String, ByVal fInfoLevelId As FINDEX_INFO_LEVELS, ByRef lpFindFileData As WIN32_FIND_DATAW, ByVal fSearchOp As FINDEX_SEARCH_OPS, lpSearchFilter As IntPtr, dwAdditionalFlags As Integer) As IntPtr
    End Function
```

## User-Defined Types:
```cs
// dwAdditionalFlags:
public const int FIND_FIRST_EX_CASE_SENSITIVE= 1; 
public const int FIND_FIRST_EX_LARGE_FETCH = 2;
```

## Sample Code:
```cs
WIN32_FIND_DATA findData;
    FINDEX_INFO_LEVELS findInfoLevel = FINDEX_INFO_LEVELS.FindExInfoStandard;
    int additionalFlags = 0;
    if (Environment.OSVersion.Version.Major >= 6)
    {
    findInfoLevel = FINDEX_INFO_LEVELS.FindExInfoBasic;
    additionalFlags = FIND_FIRST_EX_LARGE_FETCH;
    }

    IntPtr hFile = FindFirstFileEx(
    pattern,
    findInfoLevel,
    out findData,
    FINDEX_SEARCH_OPS.FindExSearchNameMatch,
    IntPtr.Zero,
    additionalFlags);
    int error = Marshal.GetLastWin32Error();

    if (hFile.ToInt32() != -1)
    {
    do
    {
        if ((findData.dwFileAttributes & FileAttributes.Directory) != FileAttributes.Directory)
        {
        Console.WriteLine("Found file {0}", findData.cFileName);
        }
    }
    while (FindNextFile(hFile, out findData));

    FindClose(hFile);
    }
```
