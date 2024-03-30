
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true, CharSet=CharSet.Auto)]
static extern bool MoveFileWithProgress(string lpExistingFileName,
   string lpNewFileName, CopyProgressRoutine lpProgressRoutine,
   IntPtr lpData, MoveFileFlags dwFlags);
```

## Sample Code:
```cs
[DllImport("kernel32.dll", SetLastError = true, CharSet = CharSet.Auto)]
    static extern bool MoveFileWithProgress(string lpExistingFileName, string lpNewFileName,
       CopyProgressRoutine lpProgressRoutine, IntPtr lpData, MoveFileFlags dwCopyFlags);

    delegate CopyProgressResult CopyProgressRoutine(
    long TotalFileSize,
    long TotalBytesTransferred,
    long StreamSize,
    long StreamBytesTransferred,
    uint dwStreamNumber,
    CopyProgressCallbackReason dwCallbackReason,
    IntPtr hSourceFile,
    IntPtr hDestinationFile,
    IntPtr lpData);

    int pbCancel;

    enum CopyProgressResult : uint
    {
    PROGRESS_CONTINUE = 0,
    PROGRESS_CANCEL = 1,
    PROGRESS_STOP = 2,
    PROGRESS_QUIET = 3
    }

    enum CopyProgressCallbackReason : uint
    {
    CALLBACK_CHUNK_FINISHED = 0x00000000,
    CALLBACK_STREAM_SWITCH = 0x00000001
    }

    [Flags]
    enum MoveFileFlags : uint
    {
    MOVE_FILE_REPLACE_EXISTSING = 0x00000001,
    MOVE_FILE_COPY_ALLOWED = 0x00000002,
    MOVE_FILE_DELAY_UNTIL_REBOOT = 0x00000004,
    MOVE_FILE_WRITE_THROUGH = 0x00000008,
    MOVE_FILE_CREATE_HARDLINK = 0x00000010, 
    MOVE_FILE_FAIL_IF_NOT_TRACKABLE = 0x00000020
    }

    private void XCopy(string oldFile, string newFile)
    {
    CopyFileEx(oldFile, newFile, new CopyProgressRoutine(this.CopyProgressHandler), IntPtr.Zero, MoveFileFlags .MOVE_FILE_REPLACE_EXISTSING|MoveFileFlags.MOVE_FILE_WRITE_THROUGH|MoveFileFlags.MOVE_FILE_COPY_ALLOWED);
    }

    private CopyProgressResult CopyProgressHandler(long total, long transferred, long streamSize, long StreamByteTrans, uint dwStreamNumber,CopyProgressCallbackReason reason, IntPtr hSourceFile, IntPtr hDestinationFile, IntPtr lpData)
    {
    return CopyProgressResult.PROGRESS_CONTINUE;
    }
```
