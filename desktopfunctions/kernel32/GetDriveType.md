
## C# Signature:
```cs
/// <summary>
  /// The GetDriveType function determines whether a disk drive is a removable, fixed, CD-ROM, RAM disk, or network drive
  /// </summary>
  /// <param name="lpRootPathName">A pointer to a null-terminated string that specifies the root directory and returns information about the disk.A trailing backslash is required. If this parameter is NULL, the function uses the root of the current directory.</param>
  [DllImport("kernel32.dll")]
  public static extern DriveType GetDriveType([MarshalAs(UnmanagedType.LPStr)] string lpRootPathName);
```

## VB Signature:
```cs
Private Declare Function GetDriveType Lib "kernel32" _
  Alias "GetDriveTypeA" (ByVal lpRootPathName As String) As Integer
```

## User-Defined Types:
```cs
public enum DriveType : uint
  {
    /// <summary>The drive type cannot be determined.</summary>
    Unknown = 0,    //DRIVE_UNKNOWN
    /// <summary>The root path is invalid, for example, no volume is mounted at the path.</summary>
    Error = 1,        //DRIVE_NO_ROOT_DIR
    /// <summary>The drive is a type that has removable media, for example, a floppy drive or removable hard disk.</summary>
    Removable = 2,    //DRIVE_REMOVABLE
    /// <summary>The drive is a type that cannot be removed, for example, a fixed hard drive.</summary>
    Fixed = 3,        //DRIVE_FIXED
    /// <summary>The drive is a remote (network) drive.</summary>
    Remote = 4,        //DRIVE_REMOTE
    /// <summary>The drive is a CD-ROM drive.</summary>
    CDROM = 5,        //DRIVE_CDROM
    /// <summary>The drive is a RAM disk.</summary>
    RAMDisk = 6        //DRIVE_RAMDISK
  }
```

## User-Defined Types:
```cs
Public Enum DriveType
    DRIVE_UNKNOWN = 0
    DRIVE_NO_ROOT_DIR = 1
    DRIVE_REMOVABLE = 2
    DRIVE_FIXED = 3
    DRIVE_REMOTE = 4
    DRIVE_CDROM = 5
    DRIVE_RAMDISK = 6
  End Enum
```

## Notes:
```cs
the above prototype fails with [MarshalAs(UnmanagedType.LPStr)]. However, this works:
```

## Notes:
```cs
public static extern DriveType GetDriveType([MarshalAs(UnmanagedType.LPTStr)] string lpRootPathName);
```

## Sample Code:
```cs
using System.Runtime.InteropServices;
using System.IO;
namespace Volume
{
class Program
{
    [DllImport("kernel32.dll")]
    public static extern DriveType GetDriveType([MarshalAs(UnmanagedType.LPStr)] string lpRootPathName);

    static void Main(string[] args)
    {
        DriveType dt = GetDriveType("D:\\");//for me this is cdrom
    }
}
}
```
