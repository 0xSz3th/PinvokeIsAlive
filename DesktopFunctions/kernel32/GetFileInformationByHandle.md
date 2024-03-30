
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
    private static extern bool GetFileInformationByHandleEx(IntPtr hFile, FILE_INFO_BY_HANDLE_CLASS infoClass, out FILE_ID_BOTH_DIR_INFO dirInfo, uint dwBufferSize);
```

## VB Signature:
```cs
Declare Function GetFileInformationByHandleEx Lib "kernel32.dll" (TODO) As TODO
```

## Sample Code:
```cs
internal static Int64 GetDirectoryId(string dir)
    {
        var handle = CreateFile(dir, FileAccess.Read, FileShare.Read, IntPtr.Zero, FileMode.Open, 0x02000000 | 0x00000080, IntPtr.Zero);
        var fileStruct = new FILE_ID_BOTH_DIR_INFO();
        GetFileInformationByHandleEx(handle, FILE_INFO_BY_HANDLE_CLASS.FileIdBothDirectoryInfo, out fileStruct, (uint)Marshal.SizeOf(fileStruct));
        CloseHandle(handle);
        var win32Error = Marshal.GetLastWin32Error();
        if (win32Error != 0)
        throw new Win32Exception();

        return fileStruct.FileId.QuadPart;
    }
```
