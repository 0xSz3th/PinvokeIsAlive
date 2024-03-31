
## C# Definition:
```cs
[Flags]
    public enum SIIGBF
    {
        SIIGBF_RESIZETOFIT = 0x00,
        SIIGBF_BIGGERSIZEOK = 0x01,
        SIIGBF_MEMORYONLY = 0x02,
        SIIGBF_ICONONLY = 0x04,
        SIIGBF_THUMBNAILONLY = 0x08,
        SIIGBF_INCACHEONLY = 0x10,
    }
```

## VB Definition:
```cs
<Flags()>  _
    Public Enum SIIGBF

        SIIGBF_RESIZETOFIT = 0
        SIIGBF_BIGGERSIZEOK = 1
        SIIGBF_MEMORYONLY = 2
        SIIGBF_ICONONLY = 4
        SIIGBF_THUMBNAILONLY = 8
        SIIGBF_INCACHEONLY = 16
    End Enum
```
