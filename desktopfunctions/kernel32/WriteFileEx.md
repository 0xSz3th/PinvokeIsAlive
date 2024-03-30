
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool WriteFileEx(IntPtr hFile, byte [] lpBuffer,
   uint nNumberOfBytesToWrite, [In] ref System.Threading.NativeOverlapped lpOverlapped,
   WriteFileCompletionDelegate lpCompletionRoutine);
```

## Sample Code:
```cs
public const int FILE_READ_DATA         = 0x0001;     // file & pipe
  public const int FILE_LIST_DIRECTORY    = 0x0001;     // directory
  public const int FILE_WRITE_DATA        = 0x0002;     // file & pipe
  public const int FILE_ADD_FILE          = 0x0002;     // directory
  public const int FILE_APPEND_DATA       = 0x0004;     // file
  public const int FILE_ADD_SUBDIRECTORY      = 0x0004;     // directory
  public const int FILE_CREATE_PIPE_INSTANCE  = 0x0004;     // named pipe
  public const int FILE_READ_EA           = 0x0008;     // file & directory
  public const int FILE_WRITE_EA          = 0x0010;     // file & directory
  public const int FILE_EXECUTE           = 0x0020;     // file
  public const int FILE_TRAVERSE          = 0x0020;     // directory
  public const int FILE_DELETE_CHILD      = 0x0040;     // directory
  public const int FILE_READ_ATTRIBUTES       = 0x0080;     // all
  public const int FILE_WRITE_ATTRIBUTES      = 0x0100;     // all

  public const long STANDARD_RIGHTS_REQUIRED  = 0x000F0000L;
  public const long READ_CONTROL          = 0x00020000L;
  public const long SYNCHRONIZE           = 0x00100000L;
  public const long STANDARD_RIGHTS_READ      = READ_CONTROL;
  public const long STANDARD_RIGHTS_WRITE     = READ_CONTROL;
  public const long STANDARD_RIGHTS_EXECUTE   = READ_CONTROL;
  public const long STANDARD_RIGHTS_ALL       = 0x001F0000L;

  public const long SPECIFIC_RIGHTS_ALL       = 0x0000FFFFL;
  public const long FILE_ALL_ACCESS = STANDARD_RIGHTS_REQUIRED | SYNCHRONIZE | 0x1FF;

  public const long FILE_GENERIC_READ     = STANDARD_RIGHTS_READ     |
    FILE_READ_DATA       |
    FILE_READ_ATTRIBUTES     |
    FILE_READ_EA         |
    SYNCHRONIZE;

  public const long FILE_GENERIC_WRITE    = STANDARD_RIGHTS_WRITE    |
    FILE_WRITE_DATA      |
    FILE_WRITE_ATTRIBUTES    |
    FILE_WRITE_EA        |
    FILE_APPEND_DATA     |
    SYNCHRONIZE;

  public const long FILE_GENERIC_EXECUTE      = STANDARD_RIGHTS_EXECUTE  |
    FILE_READ_ATTRIBUTES     |
    FILE_EXECUTE         |
    SYNCHRONIZE;

  public const int FILE_SHARE_READ             = 0x00000001;  
  public const int FILE_SHARE_WRITE            = 0x00000002;  
  public const int FILE_SHARE_DELETE           = 0x00000004;  
  public const int FILE_ATTRIBUTE_READONLY         = 0x00000001;
  public const int FILE_ATTRIBUTE_HIDDEN           = 0x00000002;
  public const int FILE_ATTRIBUTE_SYSTEM           = 0x00000004;
  public const int FILE_ATTRIBUTE_DIRECTORY        = 0x00000010;
  public const int FILE_ATTRIBUTE_ARCHIVE          = 0x00000020;
  public const int FILE_ATTRIBUTE_DEVICE           = 0x00000040;
  public const int FILE_ATTRIBUTE_NORMAL           = 0x00000080;
  public const int FILE_ATTRIBUTE_TEMPORARY        = 0x00000100;
  public const int FILE_ATTRIBUTE_SPARSE_FILE      = 0x00000200;
  public const int FILE_ATTRIBUTE_REPARSE_POINT    = 0x00000400;
  public const int FILE_ATTRIBUTE_COMPRESSED       = 0x00000800;
  public const int FILE_ATTRIBUTE_OFFLINE          = 0x00001000;
  public const int FILE_ATTRIBUTE_NOT_CONTENT_INDEXED  = 0x00002000;
  public const int FILE_ATTRIBUTE_ENCRYPTED        = 0x00004000;
  public const int FILE_NOTIFY_CHANGE_FILE_NAME    = 0x00000001;
  public const int FILE_NOTIFY_CHANGE_DIR_NAME     = 0x00000002;
  public const int FILE_NOTIFY_CHANGE_ATTRIBUTES       = 0x00000004;
  public const int FILE_NOTIFY_CHANGE_SIZE         = 0x00000008;
  public const int FILE_NOTIFY_CHANGE_LAST_WRITE       = 0x00000010;
  public const int FILE_NOTIFY_CHANGE_LAST_ACCESS      = 0x00000020;
  public const int FILE_NOTIFY_CHANGE_CREATION     = 0x00000040;
  public const int FILE_NOTIFY_CHANGE_SECURITY     = 0x00000100;
  public const int FILE_ACTION_ADDED           = 0x00000001;   
  public const int FILE_ACTION_REMOVED         = 0x00000002;  
  public const int FILE_ACTION_MODIFIED        = 0x00000003; 
  public const int FILE_ACTION_RENAMED_OLD_NAME    = 0x00000004;
  public const int FILE_ACTION_RENAMED_NEW_NAME    = 0x00000005;
  public const int  MAILSLOT_NO_MESSAGE        = -1;
  public const int MAILSLOT_WAIT_FOREVER           = -1;
  public const int FILE_CASE_SENSITIVE_SEARCH      = 0x00000001;
  public const int FILE_CASE_PRESERVED_NAMES       = 0x00000002;
  public const int FILE_UNICODE_ON_DISK        = 0x00000004;
  public const int FILE_PERSISTENT_ACLS        = 0x00000008;
  public const int FILE_FILE_COMPRESSION           = 0x00000010;
  public const int FILE_VOLUME_QUOTAS          = 0x00000020;
  public const int FILE_SUPPORTS_SPARSE_FILES      = 0x00000040;
  public const int FILE_SUPPORTS_REPARSE_POINTS    = 0x00000080;
  public const int FILE_SUPPORTS_REMOTE_STORAGE    = 0x00000100;
  public const int FILE_VOLUME_IS_COMPRESSED       = 0x00008000;
  public const int FILE_SUPPORTS_OBJECT_IDS        = 0x00010000;
  public const int FILE_SUPPORTS_ENCRYPTION        = 0x00020000;
  public const int FILE_NAMED_STREAMS          = 0x00040000;
  public const int FILE_READ_ONLY_VOLUME           = 0x00080000;
  public const int CREATE_ALWAYS               = 2;

  public delegate void WriteFileCompletionDelegate(UInt32 dwErrorCode,
    UInt32 dwNumberOfBytesTransfered, ref NativeOverlapped lpOverlapped);

  [DllImport("kernel32.dll", SetLastError=true)]
  static extern bool WriteFileEx(IntPtr hFile, byte [] lpBuffer,
    uint nNumberOfBytesToWrite, [In] ref NativeOverlapped lpOverlapped,
    WriteFileCompletionDelegate lpCompletionRoutine);

  [DllImport("kernel32.dll", SetLastError=true)]
  static extern IntPtr CreateFile(string lpFileName, uint dwDesiredAccess,
    uint dwShareMode, IntPtr lpSecurityAttributes, uint dwCreationDisposition,
    uint dwFlagsAndAttributes, IntPtr hTemplateFile);

  [DllImport("kernel32.dll", SetLastError=true)]
  static extern bool CloseHandle(IntPtr hObject);

  [STAThread]
  static void Main(string[] args)
  {
    IntPtr hfile;
    hfile = CreateFile(@"history.txt", (UInt32)FILE_ALL_ACCESS, FILE_SHARE_WRITE, IntPtr.Zero, CREATE_ALWAYS, FILE_ATTRIBUTE_NORMAL, IntPtr.Zero);

    NativeOverlapped ol = new NativeOverlapped();
    WriteFileEx(hfile, new byte[] { (byte)'t', (byte)'e', (byte)'s', (byte)'t' }, 4, ref ol, new WriteFileCompletionDelegate(Class1.callback));
    CloseHandle(hfile);
  }

  private static void callback(UInt32 dwErrorCode, UInt32 dwNumberOfBytesTransfered, ref NativeOverlapped lpOverlapped)
  {
    Console.Write("In the callback");
    Console.Read();
  }
```
