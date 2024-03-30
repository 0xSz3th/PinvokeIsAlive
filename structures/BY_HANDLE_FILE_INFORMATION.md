
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, Pack=4)]
struct BY_HANDLE_FILE_INFORMATION {
        public uint FileAttributes;
        public FILETIME CreationTime;
        public FILETIME LastAccessTime;
        public FILETIME LastWriteTime;
        public uint VolumeSerialNumber;
        public uint FileSizeHigh;
        public uint FileSizeLow;
        public uint NumberOfLinks;
        public uint FileIndexHigh;
        public uint FileIndexLow;
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Explicit)> _
Structure BY_HANDLE_FILE_INFORMATION 
  <FieldOffset(0)> Public dwFileAttributes As Int32
  <FieldOffset(4)> Public ftCreationTime As Int64         ' FILETIME
  <FieldOffset(12)> Public ftLastAccessTime As Int64      ' FILETIME
  <FieldOffset(20)> Public ftLastWriteTime As Int64       ' FILETIME
  <FieldOffset(28)> Public dwVolumeSerialNumber As Int32
  <FieldOffset(32)> Public nFileSizeHigh As Int32
  <FieldOffset(36)> Public nFileSizeLow As Int32
  <FieldOffset(40)> Public nNumberOfLinks As Int32
  <FieldOffset(44)> Public nFileIndexHigh As Int32
  <FieldOffset(48)> Public nFileIndexLow As Int32
End Structure
```

## VB Definition:
```cs
[<Struct>]
[<StructLayout(LayoutKind.Sequential)>]    
type BY_HANDLE_FILE_INFORMATION =
    val mutable FileAttributes:UInt32 
    val mutable CreationTime:FILETIME 
    val mutable LastAccessTime:FILETIME 
    val mutable LastWriteTime:FILETIME
    val mutable VolumeSerialNumber:UInt32
    val mutable FileSizeHigh:UInt32
    val mutable FileSizeLow:UInt32
    val mutable NumberOfLinks:UInt32
    val mutable FileIndexHigh:UInt32
    val mutable FileIndexLow:UInt32
```
