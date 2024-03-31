
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, Pack=4, CharSet=CharSet.Unicode)]
    public struct CATEGORYINFO
    {
        public Guid catid;
        public uint lcid;
        [MarshalAs(UnmanagedType.ByValTStr, SizeConst=128)]
        public string szDescription;
    }
```

## VB Definition:
```cs
Structure CATEGORYINFO 
   Public TODO
End Structure
```
