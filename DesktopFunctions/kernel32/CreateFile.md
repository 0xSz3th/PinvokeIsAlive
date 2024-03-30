
## C# Signature (final):
```cs
[DllImport("kernel32.dll", CharSet = CharSet.Auto, SetLastError = true)]
public static extern IntPtr CreateFile(
     [MarshalAs(UnmanagedType.LPTStr)] string filename,
     [MarshalAs(UnmanagedType.U4)] FileAccess access,
     [MarshalAs(UnmanagedType.U4)] FileShare share,
     IntPtr securityAttributes, // optional SECURITY_ATTRIBUTES struct or IntPtr.Zero
     [MarshalAs(UnmanagedType.U4)] FileMode creationDisposition,
     [MarshalAs(UnmanagedType.U4)] FileAttributes flagsAndAttributes,
     IntPtr templateFile);

[DllImport("kernel32.dll", CharSet = CharSet.Ansi, SetLastError = true)]
public static extern IntPtr CreateFileA(
     [MarshalAs(UnmanagedType.LPStr)] string filename,
     [MarshalAs(UnmanagedType.U4)] FileAccess access,
     [MarshalAs(UnmanagedType.U4)] FileShare share,
     IntPtr securityAttributes,
     [MarshalAs(UnmanagedType.U4)] FileMode creationDisposition,
     [MarshalAs(UnmanagedType.U4)] FileAttributes flagsAndAttributes,
     IntPtr templateFile);

[DllImport("kernel32.dll", CharSet = CharSet.Unicode, SetLastError = true)]
public static extern IntPtr CreateFileW(
     [MarshalAs(UnmanagedType.LPWStr)] string filename,
     [MarshalAs(UnmanagedType.U4)] FileAccess access,
     [MarshalAs(UnmanagedType.U4)] FileShare share,
     IntPtr securityAttributes,
     [MarshalAs(UnmanagedType.U4)] FileMode creationDisposition,
     [MarshalAs(UnmanagedType.U4)] FileAttributes flagsAndAttributes,
     IntPtr templateFile);
```

## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true, CharSet = CharSet.Auto)]
static extern SafeFileHandle CreateFile(
    string lpFileName,
    [MarshalAs(UnmanagedType.U4)] FileAccess dwDesiredAccess,
    [MarshalAs(UnmanagedType.U4)] FileShare dwShareMode,
    IntPtr lpSecurityAttributes,
    [MarshalAs(UnmanagedType.U4)] FileMode dwCreationDisposition,
    [MarshalAs(UnmanagedType.U4)] FileAttributes dwFlagsAndAttributes,
    IntPtr hTemplateFile);
```

## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true, CharSet=CharSet.Auto)]
public static extern SafeFileHandle CreateFile(
   string lpFileName,
   EFileAccess dwDesiredAccess,
   EFileShare dwShareMode,
   IntPtr lpSecurityAttributes,
   ECreationDisposition dwCreationDisposition,
   EFileAttributes dwFlagsAndAttributes,
   IntPtr hTemplateFile);
```

## VB.Net Signature (VB2008 style):
```cs
<System.Runtime.InteropServices.DllImport("kernel32.dll", SetLastError:=True, CharSet:=System.Runtime.InteropServices.CharSet.Auto)> _
    Friend Function CreateFile(ByVal lpFileName As String, _
    ByVal dwDesiredAccess As EFileAccess, _
    ByVal dwShareMode As EFileShare, _
    ByVal lpSecurityAttributes As IntPtr, _
    ByVal dwCreationDisposition As ECreationDisposition, _
    ByVal dwFlagsAndAttributes As EFileAttributes, _
    ByVal hTemplateFile As IntPtr) As Microsoft.Win32.SafeHandles.SafeFileHandle
    End Function
```

## VBA Signature:
```cs
Private Declare PtrSafe Function CreateFileA Lib "kernel32.dll" (ByVal lpFileName As String, _
    ByVal dwDesiredAccess As LongPtr, _
    ByVal dwShareMode As LongPtr, _
    ByVal lpSecurityAttributes As LongPtr, _
    ByVal dwCreationDisposition As LongPtr, _
    ByVal dwFlagsAndAttributes As LongPtr, _
    ByVal hTemplateFile As LongPtr) _
    As LongPtr
```

## PowerShell (.NET Reflection Style):
```cs
$Domain = [AppDomain]::CurrentDomain
$DynAssembly = New-Object System.Reflection.AssemblyName("DynamicAssembly")
$AssemblyBuilder = $Domain.DefineDynamicAssembly($DynAssembly, [System.Reflection.Emit.AssemblyBuilderAccess]::Run)
$ModuleBuilder = $AssemblyBuilder.DefineDynamicModule("DynamicModule", $False)
$TypeBuilder = $ModuleBuilder.DefineType("kernel32", "Public, Class")

# Define the CreateFile Method
$CreateFileMethod = $TypeBuilder.DefineMethod(
     "CreateFile", # Method Name
     [System.Reflection.MethodAttributes] "Public, Static", # Method Attributes
     [IntPtr], # Method Return Type
     [Type[]] @(
         [String], # lpFileName
         [UInt32], # dwDesiredAccess
         [UInt32], # dwShareMode
         [IntPtr], # SecurityAttributes
         [UInt32], # dwCreationDisposition
         [UInt32], # dwFlagsAndAttributes
         [IntPtr] # hTemplateFile
     )
) # Method Parameters

# Import DLL
$CreateFileDllImport = [System.Runtime.InteropServices.DllImportAttribute].GetConstructor(@([String]))

# Define Fields
$CreateFileFieldArray = [System.Reflection.FieldInfo[]] @(
     [System.Runtime.InteropServices.DllImportAttribute].GetField("EntryPoint"),
     [System.Runtime.InteropServices.DllImportAttribute].GetField("PreserveSig"),
     [System.Runtime.InteropServices.DllImportAttribute].GetField("SetLastError"),
     [System.Runtime.InteropServices.DllImportAttribute].GetField("CallingConvention"),
     [System.Runtime.InteropServices.DllImportAttribute].GetField("CharSet")
)

# Define Values for the fields
$CreateFileFieldValueArray = [Object[]] @(
     "CreateFile",
     $True,
     $True,
     [System.Runtime.InteropServices.CallingConvention]::Winapi,
     [System.Runtime.InteropServices.CharSet]::Auto
)

# Create a Custom Attribute and add to our Method
$CreateFileCustomAttribute = New-Object System.Reflection.Emit.CustomAttributeBuilder(
     $CreateFileDllImport,
     @("kernel32.dll"),
     $CreateFileFieldArray,
     $CreateFileFieldValueArray
)
$CreateFileMethod.SetCustomAttribute($CreateFileCustomAttribute)

# Create the Type within our Module
$Kernel32 = $TypeBuilder.CreateType()

# Use the Method
$Kernel32::CreateFile(\\.\PHYSICALDRIVE0, [System.IO.FileAccess]::Read, [System.IO.FileShare]::Read, [System.IntPtr]::Zero, [System.IO.FileMode]::Open, [System.UInt32]0x02000000 )
```

## Powershell :
```cs
$signature = @'
[DllImport("kernel32.dll", CharSet = CharSet.Unicode, SetLastError = true)]
public static extern IntPtr CreateFileW(
      string filename,
      System.IO.FileAccess access,
      System.IO.FileShare share,
      IntPtr securityAttributes,
      System.IO.FileMode creationDisposition,
      uint flagsAndAttributes,
      IntPtr templateFile);
'@

$createFile = Add-Type -MemberDefinition $signature -Name 'CreateFile' -Namespace 'pinvoke' -PassThru

# example usage for read access to a directory
$createFile[0]::CreateFileW('\\?\C:\path\to\dir', [System.IO.FileAccess]::Read, [System.IO.FileShare]::Read, [System.IntPtr]::Zero, [System.IO.FileMode]::Open, [System.UInt32]0x02000000, [System.IntPtr]::Zero
# method returns handle ID
```

## User-Defined Types:
```cs
[Flags]
    enum EFileAccess : uint
    {
        //
        // Standart Section
        //

        AccessSystemSecurity = 0x1000000,   // AccessSystemAcl access type
        MaximumAllowed = 0x2000000,     // MaximumAllowed access type

        Delete = 0x10000,
        ReadControl = 0x20000,
        WriteDAC = 0x40000,
        WriteOwner = 0x80000,
        Synchronize = 0x100000,

        StandardRightsRequired = 0xF0000,
        StandardRightsRead = ReadControl,
        StandardRightsWrite = ReadControl,
        StandardRightsExecute = ReadControl,
        StandardRightsAll = 0x1F0000,
        SpecificRightsAll = 0xFFFF,

        FILE_READ_DATA = 0x0001,        // file & pipe
        FILE_LIST_DIRECTORY = 0x0001,       // directory
        FILE_WRITE_DATA = 0x0002,       // file & pipe
        FILE_ADD_FILE = 0x0002,         // directory
        FILE_APPEND_DATA = 0x0004,      // file
        FILE_ADD_SUBDIRECTORY = 0x0004,     // directory
        FILE_CREATE_PIPE_INSTANCE = 0x0004, // named pipe
        FILE_READ_EA = 0x0008,          // file & directory
        FILE_WRITE_EA = 0x0010,         // file & directory
        FILE_EXECUTE = 0x0020,          // file
        FILE_TRAVERSE = 0x0020,         // directory
        FILE_DELETE_CHILD = 0x0040,     // directory
        FILE_READ_ATTRIBUTES = 0x0080,      // all
        FILE_WRITE_ATTRIBUTES = 0x0100,     // all

        //
        // Generic Section
        //

        GenericRead = 0x80000000,
        GenericWrite = 0x40000000,
        GenericExecute = 0x20000000,
        GenericAll = 0x10000000,

        SPECIFIC_RIGHTS_ALL = 0x00FFFF,
        FILE_ALL_ACCESS =
        StandardRightsRequired |
        Synchronize | 
        0x1FF,

        FILE_GENERIC_READ =
        StandardRightsRead |
        FILE_READ_DATA |
        FILE_READ_ATTRIBUTES |
        FILE_READ_EA |
        Synchronize,

        FILE_GENERIC_WRITE =
        StandardRightsWrite |
        FILE_WRITE_DATA |
        FILE_WRITE_ATTRIBUTES |
        FILE_WRITE_EA |
        FILE_APPEND_DATA |
        Synchronize,

        FILE_GENERIC_EXECUTE = 
        StandardRightsExecute |
          FILE_READ_ATTRIBUTES |
          FILE_EXECUTE |
          Synchronize
    }

[Flags]
public enum EFileShare : uint
{
   /// <summary>
   /// 
   /// </summary>
   None = 0x00000000,
   /// <summary>
   /// Enables subsequent open operations on an object to request read access. 
   /// Otherwise, other processes cannot open the object if they request read access. 
   /// If this flag is not specified, but the object has been opened for read access, the function fails.
   /// </summary>
   Read = 0x00000001,
   /// <summary>
   /// Enables subsequent open operations on an object to request write access. 
   /// Otherwise, other processes cannot open the object if they request write access. 
   /// If this flag is not specified, but the object has been opened for write access, the function fails.
   /// </summary>
   Write = 0x00000002,
   /// <summary>
   /// Enables subsequent open operations on an object to request delete access. 
   /// Otherwise, other processes cannot open the object if they request delete access.
   /// If this flag is not specified, but the object has been opened for delete access, the function fails.
   /// </summary>
   Delete = 0x00000004
}

public enum ECreationDisposition : uint
{
   /// <summary>
   /// Creates a new file. The function fails if a specified file exists.
   /// </summary>
   New = 1,
   /// <summary>
   /// Creates a new file, always. 
   /// If a file exists, the function overwrites the file, clears the existing attributes, combines the specified file attributes, 
   /// and flags with FILE_ATTRIBUTE_ARCHIVE, but does not set the security descriptor that the SECURITY_ATTRIBUTES structure specifies.
   /// </summary>
   CreateAlways = 2,
   /// <summary>
   /// Opens a file. The function fails if the file does not exist. 
   /// </summary>
   OpenExisting = 3,
   /// <summary>
   /// Opens a file, always. 
   /// If a file does not exist, the function creates a file as if dwCreationDisposition is CREATE_NEW.
   /// </summary>
   OpenAlways = 4,
   /// <summary>
   /// Opens a file and truncates it so that its size is 0 (zero) bytes. The function fails if the file does not exist.
   /// The calling process must open the file with the GENERIC_WRITE access right. 
   /// </summary>
   TruncateExisting = 5
}

[Flags]
public enum EFileAttributes : uint
{
   Readonly         = 0x00000001,
   Hidden           = 0x00000002,
   System           = 0x00000004,
   Directory        = 0x00000010,
   Archive          = 0x00000020,
   Device           = 0x00000040,
   Normal           = 0x00000080,
   Temporary        = 0x00000100,
   SparseFile       = 0x00000200,
   ReparsePoint     = 0x00000400,
   Compressed       = 0x00000800,
   Offline          = 0x00001000,
   NotContentIndexed= 0x00002000,
   Encrypted        = 0x00004000,
   Write_Through    = 0x80000000,
   Overlapped       = 0x40000000,
   NoBuffering      = 0x20000000,
   RandomAccess     = 0x10000000,
   SequentialScan   = 0x08000000,
   DeleteOnClose    = 0x04000000,
   BackupSemantics  = 0x02000000,
   PosixSemantics   = 0x01000000,
   OpenReparsePoint = 0x00200000,
   OpenNoRecall     = 0x00100000,
   FirstPipeInstance= 0x00080000
}
```

## User-Defined Types (VB2008 style):
```cs
Friend Structure STORAGE_DEVICE_NUMBER
     Friend DeviceType As Integer
     Friend DeviceNumber As Integer
     Friend PartitionNumber As Integer
End Structure

Friend Enum EFileAccess As System.Int32
     ''
     ''  The following are masks for the predefined standard access types
     ''

     DELETE = &H10000
     READ_CONTROL = &H20000
     WRITE_DAC = &H40000
     WRITE_OWNER = &H80000
     SYNCHRONIZE = &H100000

     STANDARD_RIGHTS_REQUIRED = &HF0000
     STANDARD_RIGHTS_READ = READ_CONTROL
     STANDARD_RIGHTS_WRITE = READ_CONTROL
     STANDARD_RIGHTS_EXECUTE = READ_CONTROL
     STANDARD_RIGHTS_ALL = &H1F0000
     SPECIFIC_RIGHTS_ALL = &HFFFF

     ''
     '' AccessSystemAcl access type
     ''

     ACCESS_SYSTEM_SECURITY = &H1000000

     ''
     '' MaximumAllowed access type
     ''

     MAXIMUM_ALLOWED = &H2000000

     ''
     ''  These are the generic rights.
     ''

     GENERIC_READ = &H80000000
     GENERIC_WRITE = &H40000000
     GENERIC_EXECUTE = &H20000000
     GENERIC_ALL = &H10000000
End Enum

Friend Enum EFileShare
     FILE_SHARE_NONE = &H0
     FILE_SHARE_READ = &H1
     FILE_SHARE_WRITE = &H2
     FILE_SHARE_DELETE = &H4
End Enum

Friend Enum ECreationDisposition
     ''' <summary>
     ''' Creates a new file, only if it does not already exist.
     ''' If the specified file exists, the function fails and the last-error code is set to ERROR_FILE_EXISTS (80).
     ''' If the specified file does not exist and is a valid path to a writable location, a new file is created.
     ''' </summary>
     CREATE_NEW = 1

     ''' <summary>
     ''' Creates a new file, always.
     ''' If the specified file exists and is writable, the function overwrites the file, the function succeeds, and last-error code is set to ERROR_ALREADY_EXISTS (183).
     ''' If the specified file does not exist and is a valid path, a new file is created, the function succeeds, and the last-error code is set to zero.
     ''' For more information, see the Remarks section of this topic.
     ''' </summary>
     CREATE_ALWAYS = 2

     ''' <summary>
     ''' Opens a file or device, only if it exists.
     ''' If the specified file or device does not exist, the function fails and the last-error code is set to ERROR_FILE_NOT_FOUND (2).
     ''' For more information about devices, see the Remarks section.
     ''' </summary>
     OPEN_EXISTING = 3

     ''' <summary>
     ''' Opens a file, always.
     ''' If the specified file exists, the function succeeds and the last-error code is set to ERROR_ALREADY_EXISTS (183).
     ''' If the specified file does not exist and is a valid path to a writable location, the function creates a file and the last-error code is set to zero.
     ''' </summary>
     OPEN_ALWAYS = 4

     ''' <summary>
     ''' Opens a file and truncates it so that its size is zero bytes, only if it exists.
     ''' If the specified file does not exist, the function fails and the last-error code is set to ERROR_FILE_NOT_FOUND (2).
     ''' The calling process must open the file with the GENERIC_WRITE bit set as part of the dwDesiredAccess parameter.
     ''' </summary>
     TRUNCATE_EXISTING = 5
End Enum

Friend Enum EFileAttributes
     FILE_ATTRIBUTE_READONLY = &H1
     FILE_ATTRIBUTE_HIDDEN = &H2
     FILE_ATTRIBUTE_SYSTEM = &H4
     FILE_ATTRIBUTE_DIRECTORY = &H10
     FILE_ATTRIBUTE_ARCHIVE = &H20
     FILE_ATTRIBUTE_DEVICE = &H40
     FILE_ATTRIBUTE_NORMAL = &H80
     FILE_ATTRIBUTE_TEMPORARY = &H100
     FILE_ATTRIBUTE_SPARSE_FILE = &H200
     FILE_ATTRIBUTE_REPARSE_POINT = &H400
     FILE_ATTRIBUTE_COMPRESSED = &H800
     FILE_ATTRIBUTE_OFFLINE = &H1000
     FILE_ATTRIBUTE_NOT_CONTENT_INDEXED = &H2000
     FILE_ATTRIBUTE_ENCRYPTED = &H4000
     FILE_ATTRIBUTE_VIRTUAL = &H10000

     'This parameter can also contain combinations of flags (FILE_FLAG_*) 
     FILE_FLAG_BACKUP_SEMANTICS = &H2000000
     FILE_FLAG_DELETE_ON_CLOSE = &H4000000
     FILE_FLAG_NO_BUFFERING = &H20000000
     FILE_FLAG_OPEN_NO_RECALL = &H100000
     FILE_FLAG_OPEN_REPARSE_POINT = &H200000
     FILE_FLAG_OVERLAPPED = &H40000000
     FILE_FLAG_POSIX_SEMANTICS = &H1000000
     FILE_FLAG_RANDOM_ACCESS = &H10000000
     FILE_FLAG_SEQUENTIAL_SCAN = &H8000000
     FILE_FLAG_WRITE_THROUGH = &H80000000
End Enum
```

## Tips & Tricks:
```cs
IntPtr ptr = CreateFile(filename,access, share,0, mode,0, IntPtr.Zero);
/* Is bad handle? INVALID_HANDLE_VALUE */
if (ptr.ToInt32() == -1)
{
    /* ask the framework to marshall the win32 error code to an exception */
    Marshal.ThrowExceptionForHR(Marshal.GetHRForLastWin32Error());
}
else
{
    return new FileStream(ptr,access);
}
```

## Microsoft .NET Framework 2.0 Changes
```cs
return new FileStream(hDrv, FileAccess.Read);
```

## Microsoft .NET Framework 2.0 Changes
```cs
[DllImport("Kernel32.dll", SetLastError = true, CharSet = CharSet.Auto)]
    static extern SafeFileHandle CreateFile(
        string fileName,
        [MarshalAs(UnmanagedType.U4)] FileAccess fileAccess,
        [MarshalAs(UnmanagedType.U4)] FileShare fileShare,
        IntPtr securityAttributes,
        [MarshalAs(UnmanagedType.U4)] FileMode creationDisposition,
        [MarshalAs(UnmanagedType.U4)] FileAttributes flags,
        IntPtr template);
```

## Microsoft .NET Framework 2.0 Changes
```cs
SafeFileHandle handle = CreateFile(Path,GENERIC_WRITE,0,
        IntPtr.Zero,OPEN_EXISTING,0,IntPtr.Zero);
    if (handle.IsInvalid)
        Marshal.ThrowExceptionForHR(Marshal.GetHRForLastWin32Error());
```

## Alternative Managed API:
```cs
[DllImport("Kernel32.dll", SetLastError = true, CharSet = CharSet.Auto)]
    static extern IntPtr CreateFile(
        string fileName,
        [MarshalAs(UnmanagedType.U4)] FileAccess fileAccess,
        [MarshalAs(UnmanagedType.U4)] FileShare fileShare,
        IntPtr securityAttributes, // optional SECURITY_ATTRIBUTES structure can be passed
        [MarshalAs(UnmanagedType.U4)] FileMode creationDisposition,
        [MarshalAs(UnmanagedType.U4)] FileAttributes flagsAndAttributes,
        IntPtr template);
```

## Alternative Managed API:
```cs
/// Sample code provided as is.
/// Sample Composed by Wijaya "Wi" T
/// References: 
/// http://www.dotnettalk.net/Needed_help_on_printing_from_C_and_printer-6941579-1297-a.html
/// http://www.dotnet247.com/247reference/msgs/16/84730.aspx
/// http://www.groupsrv.com/dotnet/viewtopic.php?t=72572
/// http://www.pinvoke.net/default.aspx/kernel32.CreateFile
///    Usage:  
///        Initialize this class in your main code (see below),
///        and walla you are now printing!
///        
///        e.g.: 
///        PrintFactory objPrintFactory = new PrintFactory();
///    Thank you:
///        Thank you all who have been contributing to printing to LPT port.
///        God Bless you! : )
///    Addt'l info:
///        Don't forget to reference:
///            using System.Runtime.InteropServices;
///            using System.IO;
///            
public class PrintFactory
{
   public const short FILE_ATTRIBUTE_NORMAL = 0x80;
   public const short INVALID_HANDLE_VALUE = -1;
   public const uint GENERIC_READ = 0x80000000;
   public const uint GENERIC_WRITE = 0x40000000;
   public const uint CREATE_NEW = 1;
   public const uint CREATE_ALWAYS = 2;
   public const uint OPEN_EXISTING = 3;        

   [DllImport("kernel32.dll", SetLastError=true)]
   static extern IntPtr CreateFile(string lpFileName, uint dwDesiredAccess,
       uint dwShareMode, IntPtr lpSecurityAttributes, uint dwCreationDisposition,
       uint dwFlagsAndAttributes, IntPtr hTemplateFile);

   public PrintFactory()
   {
      IntPtr ptr = CreateFile("LPT1", GENERIC_WRITE, 0, 
               IntPtr.Zero, OPEN_EXISTING, 0, IntPtr.Zero);

      /* Is bad handle? INVALID_HANDLE_VALUE */
      if (ptr.ToInt32() == -1)
      {
     /* ask the framework to marshall the win32 error code to an exception */
     Marshal.ThrowExceptionForHR(Marshal.GetHRForLastWin32Error());
      }
      else
      {                                    
     String Temp = "This is a test print"; 
     //This is the cut command on Star TSP 600 Printer
     char[] prnCmdCut = {(char)27, (char)100, (char)51};                
     FileStream lpt = new FileStream(ptr,FileAccess.ReadWrite); 
     Byte[] Buff = new Byte[1024]; 
     //Check to see if your printer support ASCII encoding or Unicode.
     //If unicode is supported, use the following:
     //Buff = System.Text.Encoding.Unicode.GetBytes(Temp);
     Buff = System.Text.Encoding.ASCII.GetBytes(Temp);
     lpt.Write(Buff,0,Buff.Length);                     
     Buff = System.Text.Encoding.ASCII.GetBytes(prnCmdCut);
     lpt.Write(Buff,0,Buff.Length); 
     lpt.Close();
       }
    }
}
```

## Alternative Managed API:
```cs
/* Sample Code provided by MertG */
/* References:              */
/*  This page,
     http://stackoverflow.com/questions/4288031/createfile-in-kernel32-dll-does-not-allow-me-to-open-a-physical-disk */

//Using directives needed:
using System.IO;
using System.Runtime.InteropServices;
using Microsoft.Win32.SafeHandles;
```

## Alternative Managed API:
```cs
//function import
[DllImport( "Kernel32.dll", SetLastError = true, CharSet = CharSet.Auto )]
    static extern SafeFileHandle CreateFile(
        string fileName,
        [MarshalAs( UnmanagedType.U4 )] FileAccess fileAccess,
        [MarshalAs( UnmanagedType.U4 )] FileShare fileShare,
        IntPtr securityAttributes,
        [MarshalAs( UnmanagedType.U4 )] FileMode creationDisposition,
        int flags,
        IntPtr template );

//function to read 
private static byte[] ReadDrive( string FileName, int sizeToRead ) {

       if ( (sizeToRead < 1) || (sizeToRead == null) ) throw new System.ArgumentException("Size parameter cannot be null or 0 or less than 0!");
        SafeFileHandle drive = CreateFile( fileName: FileName,
                     fileAccess: FileAccess.Read,
                     fileShare: FileShare.Write | FileShare.Read | FileShare.Delete,
                     securityAttributes: IntPtr.Zero,
                     creationDisposition: FileMode.Open,
                     flags: 4, //with this also an enum can be used. (as described above as EFileAttributes)
                     template: IntPtr.Zero );
        if (drive.IsInvalid) {
        throw new IOException( "Unable to access drive. Win32 Error Code " + Marshal.GetLastWin32Error() );
           //if get windows error code 5 this means access denied. You must try to run the program as admin privileges.
        }    

        FileStream diskStreamToRead = new FileStream( drive, FileAccess.Read );
        byte[] buf = new byte[512];
        diskStreamToRead.Read( buf, 0, 512 );
        try { diskStreamToRead.Close(); } catch { }
        try { drive.Close(); } catch { }
        return buf;
    }
```

## Alternative Managed API:
```cs
//function to write
private void writeToDisk( string lpFileName, byte[] dataToWrite ) {
    if (dataToWrite == null) throw new System.ArgumentException("dataToWrite parameter cannot be null!");

    SafeFileHandle drive = CreateFile( fileName: FileName,
                     fileAccess: FileAccess.Write,
                     fileShare: FileShare.Write | FileShare.Read | FileShare.Delete,
                     securityAttributes: IntPtr.Zero,
                     creationDisposition: FileMode.Open,
                     flags: 4, //with this also an enum can be used. (as described above as EFileAttributes)
                     template: IntPtr.Zero );

    FileStream diskStreamToWrite = new FileStream( drive, FileAccess.Write );
    diskStreamToWrite.Write( dataToWrite, 0, dataToWrite.Length );
    try { diskStreamToWrite.Close(); } catch { }
     try { drive.Close(); } catch { }
}
```
