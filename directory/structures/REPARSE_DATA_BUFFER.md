
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
struct REPARSE_DATA_BUFFER {
     uint ReparseTag;
     ushort ReparseDataLength;
     ushort Reserved;
     ushort SubstituteNameOffset;
     ushort SubstituteNameLength;
     ushort PrintNameOffset;
     ushort PrintNameLength;
     [MarshalAs(UnmanagedType.ByValArray, SizeConst = 0x3FF0)]
     byte[] PathBuffer;
}
```

## Members
```cs
ReparseTag
    Reparse point tag. Must be a Microsoft reparse point tag.
ReparseDataLength
    Size, in bytes, of the data after the Reserved member. This can be calculated by:
       (4 * sizeof(ushort)) + SubstituteNameLength + PrintNameLength + 
       (namesAreNullTerminated ? 2 * sizeof(char) : 0);
Reserved
    Reserved; do not use. 
SubstituteNameOffset
    Offset, in bytes, of the substitute name string in the PathBuffer array.
SubstituteNameLength
    Length, in bytes, of the substitute name string. If this string is null-terminated,
    SubstituteNameLength does not include space for the null character. 
PrintNameOffset
    Offset, in bytes, of the print name string in the PathBuffer array.
PrintNameLength
    Length, in bytes, of the print name string. If this string is null-terminated,
    PrintNameLength does not include space for the null character. 
PathBuffer
    A buffer containing the unicode-encoded path string. The path string contains
    the substitute name string and print name string.
```

## Notes:
```cs
REPARSE_DATA_BUFFER_HEADER_SIZE + ReparseDataLength
```

## Notes:
```cs
REPARSE_DATA_BUFFER_HEADER_SIZE = sizeof(uint) + 2 * sizeof(ushort)
```

## C# Alternative Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
internal struct REPARSE_DATA_BUFFER
{
  internal uint ReparseTag;
  internal ushort ReparseDataLength;
  ushort Reserved;
  internal ushort SubstituteNameOffset;
  internal ushort SubstituteNameLength;
  internal ushort PrintNameOffset;
  internal ushort PrintNameLength;
  [MarshalAs(UnmanagedType.ByValTStr,SizeConst=500)]
  internal string PathBuffer;
}
```

## Example Code:
```cs
using System;
using System.Collections.Generic;
using System.Text;
using System.Runtime.InteropServices;
using System.IO;

namespace Situs
{
    enum ReparseTagType : uint
    {
    IO_REPARSE_TAG_MOUNT_POINT = (0xA0000003),
    IO_REPARSE_TAG_HSM = (0xC0000004),
    IO_REPARSE_TAG_SIS = (0x80000007),
    IO_REPARSE_TAG_DFS = (0x8000000A),
    IO_REPARSE_TAG_SYMLINK = (0xA000000C),
    IO_REPARSE_TAG_DFSR = (0x80000012),
    }

    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
    internal struct REPARSE_DATA_BUFFER
    {
    internal uint ReparseTag;
    internal ushort ReparseDataLength;
    ushort Reserved;
    internal ushort SubstituteNameOffset;
    internal ushort SubstituteNameLength;
    internal ushort PrintNameOffset;
    internal ushort PrintNameLength;
    [MarshalAs(UnmanagedType.ByValTStr,SizeConst=100)]
    internal string PathBuffer;
    }

    class Program
    {
    // See the PInvoke definition of DeviceIoControl for EIOControlCode
    [DllImport("kernel32.dll", SetLastError = true, CharSet = CharSet.Unicode)]
    internal static extern bool DeviceIoControl(
        IntPtr hDevice,
        EIOControlCode dwIoControlCode,
        //REPARSE_DATA_BUFFER InBuffer,
        IntPtr InBuffer,
        int nInBufferSize,
        IntPtr OutBuffer,
        int nOutBufferSize,
        ref int pBytesReturned,
        IntPtr lpOverlapped
    );

    // See pinvoke definition for CreateFile for the various Enums.
    [DllImport("kernel32.dll", SetLastError = true, CharSet = CharSet.Unicode)]
    internal static extern IntPtr CreateFile(
       string lpFileName,
       EFileAccess dwDesiredAccess,
       EFileShare dwShareMode,
       IntPtr lpSecurityAttributes,
       ECreationDisposition dwCreationDisposition,
       EFileAttributes dwFlagsAndAttributes,
       IntPtr hTemplateFile);

    // Usage: rpp.exe <TargetDevice> <MountPointPath>
    // Eg: rpp \??\CdRom0\ C:\Mnt\MP0
    static void Main(string[] args)
    {
        const int ReparseHeaderSize = sizeof(uint) + sizeof(ushort) + sizeof(ushort);

        REPARSE_DATA_BUFFER rdb = new REPARSE_DATA_BUFFER();
        rdb.ReparseTag = (uint)ReparseTagType.IO_REPARSE_TAG_MOUNT_POINT;

        String target = args[0];

        // Setup the string information
        ushort targetLenBytes = (ushort)(target.Length * sizeof(char));
        rdb.ReparseDataLength = (ushort)(targetLenBytes + 12);
        rdb.SubstituteNameLength = targetLenBytes;
        rdb.PrintNameOffset = (ushort)(targetLenBytes + 2);
        rdb.PathBuffer = target;

        // Make sure we have a folder, change to suite yourt needs!
        String rppFolder = args[1];
        if (Directory.Exists(rppFolder))
        Directory.Delete(rppFolder, true);
        Directory.CreateDirectory(rppFolder);

        // Open the file to with correct access to write the Reparse Point
        IntPtr hMP = CreateFile(rppFolder
        , EFileAccess.GenericWrite
        , EFileShare.Read | EFileShare.Write | EFileShare.Delete
        , IntPtr.Zero
        , ECreationDisposition.OpenExisting
        , EFileAttributes.BackupSemantics | EFileAttributes.OpenReparsePoint
        , IntPtr.Zero);

        // The size of the data we are passing into the FSCTL.
        int dataSize = rdb.ReparseDataLength + ReparseHeaderSize;

        IntPtr pMem = Marshal.AllocHGlobal(Marshal.SizeOf(rdb));
        try
        {
        Marshal.StructureToPtr(rdb, pMem, false);

        // Set the reparse point.
        int bytesReturned = 0;
        bool rc = DeviceIoControl(hMP
            , EIOControlCode.FsctlSetReparsePoint
            //, rdb
            , pMem
            , dataSize
            , IntPtr.Zero
            , 0
            , ref bytesReturned
            , IntPtr.Zero);
        if (!rc)
        {
            int err = Marshal.GetLastWin32Error();
            Console.WriteLine("Failed to set reparse point: 0x{0:X}", err);
        }
        }
        finally
        {
        Marshal.FreeHGlobal(pMem);
        }
    }
    }
}
```
