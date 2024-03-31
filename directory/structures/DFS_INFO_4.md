
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Unicode)]
struct DFS_INFO_4 {
        [MarshalAs(UnmanagedType.LPWStr)] public string EntryPath;    // Dfs name for the top of this volume 
        [MarshalAs(UnmanagedType.LPWStr)] public string Comment;    // Comment for this volume
        public int State;                                            // State of this volume, one of DFS_VOLUME_STATE_*
        public int Timeout;                                            // Timeout, in seconds, of this junction point
        public Guid GUID;                                            // Guid of this junction point
        public int NumberOfStorages;                                // Number of storage servers for this volume
        public IntPtr Storage;                                        // An array (of NumberOfStorages elements) of storage-specific information.
}
```

## VB Definition:
```cs
Structure DFS_INFO_4 
   Public TODO
End Structure
```
