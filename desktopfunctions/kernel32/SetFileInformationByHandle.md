
## C# Signature:
```cs
enum FileInformationClass : int
    {
        FileBasicInfo = 0,
        FileStandardInfo = 1,
        FileNameInfo = 2,
        FileRenameInfo = 3,
        FileDispositionInfo = 4,
        FileAllocationInfo = 5,
        FileEndOfFileInfo = 6,
        FileStreamInfo = 7,
        FileCompressionInfo = 8,
        FileAttributeTagInfo = 9,
        FileIdBothDirectoryInfo = 10, // 0xA
        FileIdBothDirectoryRestartInfo = 11, // 0xB
        FileIoPriorityHintInfo = 12, // 0xC
        FileRemoteProtocolInfo = 13, // 0xD
        FileFullDirectoryInfo = 14, // 0xE
        FileFullDirectoryRestartInfo = 15, // 0xF
        FileStorageInfo = 16, // 0x10
        FileAlignmentInfo = 17, // 0x11
        FileIdInfo = 18, // 0x12
        FileIdExtdDirectoryInfo = 19, // 0x13
        FileIdExtdDirectoryRestartInfo = 20, // 0x14
    }
    [StructLayout(LayoutKind.Sequential)]
    private struct FILE_BASIC_INFO
    {
        public Int64 CreationTime;
        public Int64 LastAccessTime;
        public Int64 LastWriteTime;
        public Int64 ChangeTime;
        public UInt32 FileAttributes;
    }
    [StructLayout(LayoutKind.Sequential)]
    struct FILE_DISPOSITION_INFO
    {
        public bool DeleteFile;
    }
    [StructLayout(LayoutKind.Sequential)]
    struct FILE_END_OF_FILE_INFO
    {
        public Int64 EndOfFile;
    }
    [StructLayout(LayoutKind.Explicit)]
    struct FileInformation
    {
        [FieldOffset(0)]
        public FILE_BASIC_INFO FILE_BASIC_INFO;
        [FieldOffset(0)]
        public FILE_DISPOSITION_INFO FILE_DISPOSITION_INFO;
        [FieldOffset(0)]
        public FILE_END_OF_FILE_INFO FILE_END_OF_FILE_INFO;
    }
    [DllImport("Kernel32.dll", SetLastError = true)]
    private static extern bool SetFileInformationByHandle(SafeHandle hFile, FileInformationClass FileInformationClass, ref FileInformation FileInformation, Int32 dwBufferSize);
```

## Sample Code:
```cs
var FileInformation = new FileInformation();
            FileInformation.FILE_DISPOSITION_INFO.DeleteFile = true;
            SetFileInformationByHandle(fileStream.SafeFileHandle, FileInformationClass.FileDispositionInfo, ref FileInformation, Marshal.SizeOf(FileInformation.FILE_DISPOSITION_INFO));
```

## Another Sample Code:
```cs
var FileInformation = new FileInformation();
            FileInformation..FILE_END_OF_FILE_INFO.EndOfFile = 1024; // 1KB.
            SetFileInformationByHandle(fileStream.SafeFileHandle, FileInformationClass.FileEndOfFileInfo, ref FileInformation, Marshal.SizeOf(FileInformation.FILE_END_OF_FILE_INFO));
```
