
## C# Signature:
```cs
[DllImport("ntdll.dll", SetLastError=true)] static extern IntPtr NtQueryInformationFile(IntPtr fileHandle, ref IO_STATUS_BLOCK IoStatusBlock, IntPtr pInfoBlock, uint length, FILE_INFORMATION_CLASS fileInformation);
```

## VB Signature:
```cs
Declare Function NtQueryInformationFile Lib "ntdll.dll" (ByVal fileHandle As IntPtr, ByRef IoStatusBlock As IO_STATUS_BLOCK, ByVal pInfoBlock As IntPtr, ByVal length As UInteger, ByVal fileInformation As FILE_INFORMATION_CLASS) As IntPtr
```

## VB User-Defined Types:
```cs
Structure IO_STATUS_BLOCK
        Dim status As UInteger
        Dim information As ULong
    End Structure
```

## VB User-Defined Types:
```cs
Enum FILE_INFORMATION_CLASS
        FileDirectoryInformation = 1
        FileFullDirectoryInformation
        FileBothDirectoryInformation
        FileBasicInformation
        FileStandardInformation
        FileInternalInformation
        FileEaInformation
        FileAccessInformation
        FileNameInformation
        FileRenameInformation
        FileLinkInformation
        FileNamesInformation
        FileDispositionInformation
        FilePositionInformation
        FileFullEaInformation
        FileModeInformation = 16
        FileAlignmentInformation
        FileAllInformation
        FileAllocationInformation
        FileEndOfFileInformation
        FileAlternateNameInformation
        FileStreamInformation
        FilePipeInformation
        FilePipeLocalInformation
        FilePipeRemoteInformation
        FileMailslotQueryInformation
        FileMailslotSetInformation
        FileCompressionInformation
        FileObjectIdInformation
        FileCompletionInformation
        FileMoveClusterInformation
        FileQuotaInformation
        FileReparsePointInformation
        FileNetworkOpenInformation
        FileAttributeTagInformation
        FileTrackingInformation
        FileIdBothDirectoryInformation
        FileIdFullDirectoryInformation
        FileValidDataLengthInformation
        FileShortNameInformation
        FileHardLinkInformation = 46
    End Enum
```

## C# User-Defined Types:
```cs
struct IO_STATUS_BLOCK
    {
        uint status;
        ulong information;
    }

    enum FILE_INFORMATION_CLASS
    {
        FileDirectoryInformation = 1,     // 1
        FileFullDirectoryInformation,     // 2
        FileBothDirectoryInformation,     // 3
        FileBasicInformation,         // 4
        FileStandardInformation,      // 5
        FileInternalInformation,      // 6
        FileEaInformation,        // 7
        FileAccessInformation,        // 8
        FileNameInformation,          // 9
        FileRenameInformation,        // 10
        FileLinkInformation,          // 11
        FileNamesInformation,         // 12
        FileDispositionInformation,       // 13
        FilePositionInformation,      // 14
        FileFullEaInformation,        // 15
        FileModeInformation = 16,     // 16
        FileAlignmentInformation,     // 17
        FileAllInformation,           // 18
        FileAllocationInformation,    // 19
        FileEndOfFileInformation,     // 20
        FileAlternateNameInformation,     // 21
        FileStreamInformation,        // 22
        FilePipeInformation,          // 23
        FilePipeLocalInformation,     // 24
        FilePipeRemoteInformation,    // 25
        FileMailslotQueryInformation,     // 26
        FileMailslotSetInformation,       // 27
        FileCompressionInformation,       // 28
        FileObjectIdInformation,      // 29
        FileCompletionInformation,    // 30
        FileMoveClusterInformation,       // 31
        FileQuotaInformation,         // 32
        FileReparsePointInformation,      // 33
        FileNetworkOpenInformation,       // 34
        FileAttributeTagInformation,      // 35
        FileTrackingInformation,      // 36
        FileIdBothDirectoryInformation,   // 37
        FileIdFullDirectoryInformation,   // 38
        FileValidDataLengthInformation,   // 39
        FileShortNameInformation,     // 40
        FileHardLinkInformation=46    // 46    
    }
```

## Sample Code:
```cs
#region interops

    struct IO_STATUS_BLOCK {
        internal uint status;
        internal ulong information;
    }
    enum FILE_INFORMATION_CLASS {
        FileDirectoryInformation = 1,        // 1
        FileFullDirectoryInformation,        // 2
        FileBothDirectoryInformation,        // 3
        FileBasicInformation,            // 4
        FileStandardInformation,        // 5
        FileInternalInformation,        // 6
        FileEaInformation,            // 7
        FileAccessInformation,            // 8
        FileNameInformation,            // 9
        FileRenameInformation,            // 10
        FileLinkInformation,            // 11
        FileNamesInformation,            // 12
        FileDispositionInformation,        // 13
        FilePositionInformation,        // 14
        FileFullEaInformation,            // 15
        FileModeInformation = 16,        // 16
        FileAlignmentInformation,        // 17
        FileAllInformation,            // 18
        FileAllocationInformation,        // 19
        FileEndOfFileInformation,        // 20
        FileAlternateNameInformation,        // 21
        FileStreamInformation,            // 22
        FilePipeInformation,            // 23
        FilePipeLocalInformation,        // 24
        FilePipeRemoteInformation,        // 25
        FileMailslotQueryInformation,        // 26
        FileMailslotSetInformation,        // 27
        FileCompressionInformation,        // 28
        FileObjectIdInformation,        // 29
        FileCompletionInformation,        // 30
        FileMoveClusterInformation,        // 31
        FileQuotaInformation,            // 32
        FileReparsePointInformation,        // 33
        FileNetworkOpenInformation,        // 34
        FileAttributeTagInformation,        // 35
        FileTrackingInformation,        // 36
        FileIdBothDirectoryInformation,        // 37
        FileIdFullDirectoryInformation,        // 38
        FileValidDataLengthInformation,        // 39
        FileShortNameInformation,        // 40
        FileHardLinkInformation = 46        // 46    
    }
    [StructLayout(LayoutKind.Explicit)]
    struct FILE_BASIC_INFORMATION {
        [FieldOffset(0)]
        internal long CreationTime;
        [FieldOffset(8)]
        internal long LastAccessTime;
        [FieldOffset(16)]
        internal long LastWriteTime;
        [FieldOffset(24)]
        internal long ChangeTime;
        [FieldOffset(32)]
        internal ulong FileAttributes;
    }
    [DllImport("ntdll.dll", SetLastError = true)]
    static extern IntPtr NtQueryInformationFile(SafeFileHandle fileHandle, ref IO_STATUS_BLOCK IoStatusBlock, IntPtr pInfoBlock, uint length, FILE_INFORMATION_CLASS fileInformation);

    #endregion interops
    #region converter of bit-wise file attributes into a list

    public static List<FileAttributes> ParseFileAttributes(ulong fileAttributes) {
        List<FileAttributes> listOfFileAttributesPresent = new List<FileAttributes>();
        FileAttributes[] allPossibleValues = new FileAttributes[] {        // per definition of FileAttributes
            FileAttributes.ReadOnly,
            FileAttributes.Hidden,
            FileAttributes.System,
            FileAttributes.Directory,
            FileAttributes.Archive,
            FileAttributes.Device,
            FileAttributes.Normal,
            FileAttributes.Temporary,
            FileAttributes.SparseFile,
            FileAttributes.ReparsePoint,
            FileAttributes.Compressed,
            FileAttributes.Offline,
            FileAttributes.NotContentIndexed,
            FileAttributes.Encrypted,
        };
        foreach(FileAttributes currentFileAttribute in allPossibleValues) {
            if((fileAttributes & (ulong)currentFileAttribute) != 0) {
                listOfFileAttributesPresent.Add(currentFileAttribute);
            }
        }
        return listOfFileAttributesPresent;
    }

    #endregion converter of bit-wise file attributes into a list
    #region change time available only thru NtQueryInformationFile and only on NTFS volume

    public static bool GetFourFileTimes(string path2file,
            out DateTime creationTime, out DateTime lastAccessTime, out DateTime lastWriteTime, out DateTime changeTime, out ulong fileAttributes, out string errMsg) {
        bool brc = false;
        creationTime = default(DateTime);
        lastAccessTime = default(DateTime);
        lastWriteTime = default(DateTime);
        changeTime = default(DateTime);
        errMsg = string.Empty;
        fileAttributes = 0;
        IntPtr p_fbi = IntPtr.Zero;
        try {
            FILE_BASIC_INFORMATION fbi = new FILE_BASIC_INFORMATION();
            IO_STATUS_BLOCK iosb = new IO_STATUS_BLOCK();
            using(FileStream fs = new FileStream(path2file, FileMode.Open, FileAccess.Read, FileShare.Read)) {
                p_fbi = Marshal.AllocHGlobal(Marshal.SizeOf(fbi));
                IntPtr iprc = NtQueryInformationFile(fs.SafeFileHandle, ref iosb, p_fbi, (uint)Marshal.SizeOf(fbi), FILE_INFORMATION_CLASS.FileBasicInformation);
                brc = iprc == IntPtr.Zero && iosb.status == 0;
                if(brc) {
                    brc = false;
                    fbi = (FILE_BASIC_INFORMATION)Marshal.PtrToStructure(p_fbi, typeof(FILE_BASIC_INFORMATION));
                    creationTime = DateTime.FromFileTime(fbi.CreationTime);
                    lastAccessTime = DateTime.FromFileTime(fbi.LastAccessTime);
                    lastWriteTime = DateTime.FromFileTime(fbi.LastWriteTime);
                    changeTime = DateTime.FromFileTime(fbi.ChangeTime);
                    fileAttributes = fbi.FileAttributes;
                    brc = true;
                }
            }
        } catch(Exception ex) {
            brc = false;                // JIC
            errMsg = ex.Message;
        } finally {
            if(p_fbi != IntPtr.Zero) { Marshal.FreeHGlobal(p_fbi); }
        }
        return brc;
    }

    #endregion change time available only thru NtQueryInformationFile and only on NTFS volume
    #region test main

    static void Main(string[] args) {
        // create a test file:
        string path2file = "test.fle";
        string contents = "contents of test.fle";
        Trace.WriteLine("path2file=" + path2file);
        using(FileStream fs = File.Create(path2file)) {
            fs.Write(Encoding.ASCII.GetBytes(contents), 0, Encoding.ASCII.GetBytes(contents).Length);
        }
        FileAttributes fileAttributesBefore = File.GetAttributes(path2file);
        Trace.Write("fileAttributesBefore=");
        foreach(FileAttributes fa1 in Nt.ParseFileAttributes((ulong)fileAttributesBefore)) {
            Trace.Write(fa1.ToString() + " ");
        }
        Trace.WriteLine("");

        // wait a little (1.5 sec) and modify test file attributes:
        Thread.Sleep(1500);
        File.SetAttributes(path2file, FileAttributes.Normal);

        Trace.WriteLine("");

        // run the test:
        DateTime creationTime, lastAccessTime, lastWriteTime, changeTime;
        ulong fileAttributesAfter;
        string errMsg;
        bool brc = false;
        brc = Nt.GetFourFileTimes(path2file, out creationTime, out lastAccessTime, out lastWriteTime, out changeTime, out fileAttributesAfter, out errMsg);

        // print results:
        if(!brc) {
            Trace.WriteLine("Error: " + errMsg);
        } else {
            Trace.Write("fileAttributesAfter=");
            foreach(FileAttributes fa1 in Nt.ParseFileAttributes(fileAttributesAfter)) {
                Trace.Write(fa1.ToString() + " ");
            }
            Trace.WriteLine("");
            Trace.WriteLine("lastWriteTime= " + lastWriteTime.ToString("o"));
            Trace.WriteLine("creationTime=  " + creationTime.ToString("o"));
            Trace.WriteLine("lastAccessTime=" + lastAccessTime.ToString("o"));
            Trace.WriteLine("changeTime=    " + changeTime.ToString("o"));
        }
    }
    //        sample printout:
    //path2file=test.fle
    //fileAttributesBefore=Archive 

    //fileAttributesAfter=Normal 
    //lastWriteTime= 2011-03-13T13:40:46.1003635-04:00
    //creationTime=  2011-03-13T13:35:17.3413635-04:00
    //lastAccessTime=2011-03-13T13:40:04.8263635-04:00
    //changeTime=    2011-03-13T13:40:47.6083635-04:00

    #endregion test main
```
