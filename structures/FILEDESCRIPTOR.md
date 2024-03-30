
## C# Definition:
```cs
[Flags]
enum FileDescriptorFlags : uint
{
       FD_CLSID         = 0x00000001,
       FD_SIZEPOINT     = 0x00000002,
       FD_ATTRIBUTES     = 0x00000004,
       FD_CREATETIME     = 0x00000008,
       FD_ACCESSTIME     = 0x00000010,
       FD_WRITESTIME     = 0x00000020,
       FD_FILESIZE     = 0x00000040,
       FD_PROGRESSUI     = 0x00004000,
       FD_LINKUI         = 0x00008000,
       FD_UNICODE        = 0x80000000 //Windows Vista and later
}

[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto)]
struct FILEDESCRIPTOR 
{
       public FileDescriptorFlags dwFlags;
       public Guid clsid;
       public System.Drawing.Size sizel;
       public System.Drawing.Point pointl;
       public UInt32 dwFileAttributes;
       public System.Runtime.InteropServices.ComTypes.FILETIME ftCreationTime;
       public System.Runtime.InteropServices.ComTypes.FILETIME ftLastAccessTime;
       public System.Runtime.InteropServices.ComTypes.FILETIME ftLastWriteTime;
       public UInt32 nFileSizeHigh;
       public UInt32 nFileSizeLow;
       [MarshalAs(UnmanagedType.ByValTStr, SizeConst=260)]
       public string cFileName;
}
```

## VB.NET Definition:
```cs
<Flags>
Public Enum FileDescriptorFlags As UInteger
    FD_CLSID = &H1
    FD_SIZEPOINT = &H2
    FD_ATTRIBUTES = &H4
    FD_CREATETIME = &H8
    FD_ACCESSTIME = &H10
    FD_WRITESTIME = &H20
    FD_FILESIZE = &H40
    FD_PROGRESSUI = &H4000
    FD_LINKUI = &H8000
    FD_UNICODE = &H80000000L

End Enum

<Runtime.InteropServices.StructLayout(System.Runtime.InteropServices.LayoutKind.Sequential, CharSet:=Runtime.InteropServices.CharSet.Auto)>
Public Structure FILEDESCRIPTOR
    Public dwFlags As FileDescriptorFlags
    Public clsid As Guid
    Public sizel As System.Drawing.Size
    Public pointl As System.Drawing.Point
    Public dwFileAttributes As UInt32
    Public ftCreationTime As System.Runtime.InteropServices.ComTypes.FILETIME
    Public ftLastAccessTime As System.Runtime.InteropServices.ComTypes.FILETIME
    Public ftLastWriteTime As System.Runtime.InteropServices.ComTypes.FILETIME
    Public nFileSizeHigh As UInt32
    Public nFileSizeLow As UInt32
    <Runtime.InteropServices.MarshalAs(Runtime.InteropServices.UnmanagedType.ByValTStr, SizeConst:=260)>
    Public cFileName As String
End Structure
```
