
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
    private struct FILE_ID_BOTH_DIR_INFO
    {
        public uint NextEntryOffset;
        public uint FileIndex;
        public LargeInteger CreationTime;
        public LargeInteger LastAccessTime;
        public LargeInteger LastWriteTime;
        public LargeInteger ChangeTime;
        public LargeInteger EndOfFile;
        public LargeInteger AllocationSize;
        public uint FileAttributes;
        public uint FileNameLength;
        public uint EaSize;
        public char ShortNameLength;
        [MarshalAsAttribute(UnmanagedType.ByValTStr, SizeConst = 12)]
        public string ShortName;
        public LargeInteger FileId;
        [MarshalAsAttribute(UnmanagedType.ByValTStr, SizeConst = 1)]
        public string FileName;
    }
```

## VB Definition:
```cs
Structure FILE_ID_BOTH_DIR_INFO 
   Public TODO
End Structure
```
