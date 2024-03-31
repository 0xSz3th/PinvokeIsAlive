
## C# Definition:
```cs
[Flags]
enum OpenFileStyle : uint {
    OF_CANCEL    = 0x00000800,  // Ignored. For a dialog box with a Cancel button, use OF_PROMPT.
    OF_CREATE    = 0x00001000,  // Creates a new file. If file exists, it is truncated to zero (0) length.
    OF_DELETE    = 0x00000200,  // Deletes a file.
    OF_EXIST     = 0x00004000,  // Opens a file and then closes it. Used to test that a file exists
    OF_PARSE     = 0x00000100,  // Fills the OFSTRUCT structure, but does not do anything else.
    OF_PROMPT    = 0x00002000,  // Displays a dialog box if a requested file does not exist 
    OF_READ      = 0x00000000,  // Opens a file for reading only.
    OF_READWRITE = 0x00000002,  // Opens a file with read/write permissions.
    OF_REOPEN    = 0x00008000,  // Opens a file by using information in the reopen buffer.

    // For MS-DOS–based file systems, opens a file with compatibility mode, allows any process on a 
    // specified computer to open the file any number of times.
    // Other efforts to open a file with other sharing modes fail. This flag is mapped to the 
    // FILE_SHARE_READ|FILE_SHARE_WRITE flags of the CreateFile function.
    OF_SHARE_COMPAT = 0x00000000,

    // Opens a file without denying read or write access to other processes.
    // On MS-DOS-based file systems, if the file has been opened in compatibility mode
    // by any other process, the function fails.
    // This flag is mapped to the FILE_SHARE_READ|FILE_SHARE_WRITE flags of the CreateFile function.
    OF_SHARE_DENY_NONE = 0x00000040, 

    // Opens a file and denies read access to other processes.
    // On MS-DOS-based file systems, if the file has been opened in compatibility mode,
    // or for read access by any other process, the function fails.
    // This flag is mapped to the FILE_SHARE_WRITE flag of the CreateFile function.
    OF_SHARE_DENY_READ = 0x00000030,

    // Opens a file and denies write access to other processes.
    // On MS-DOS-based file systems, if a file has been opened in compatibility mode,
    // or for write access by any other process, the function fails.
    // This flag is mapped to the FILE_SHARE_READ flag of the CreateFile function.
    OF_SHARE_DENY_WRITE = 0x00000020,

    // Opens a file with exclusive mode, and denies both read/write access to other processes.
    // If a file has been opened in any other mode for read/write access, even by the current process,
    // the function fails.
    OF_SHARE_EXCLUSIVE = 0x00000010,

    // Verifies that the date and time of a file are the same as when it was opened previously.
    // This is useful as an extra check for read-only files.
    OF_VERIFY = 0x00000400,

    // Opens a file for write access only.
    OF_WRITE = 0x00000001
```

## VB Definition:
```cs
Enum OpenFileStyle
   TODO
End Enum
```
