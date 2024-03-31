
## C# Definition:
```cs
[Flags]
enum MIIM {
     BITMAP     = 0x00000080,
     CHECKMARKS = 0x00000008,
     DATA       = 0x00000020,
     FTYPE      = 0x00000100,
     ID     = 0x00000002,
     STATE      = 0x00000001,
     STRING     = 0x00000040,
     SUBMENU    = 0x00000004,
     TYPE       = 0x00000010
}
```

## VB Definition:
```cs
<Flags>
Enum MIIM
    BITMAP     = &H00000080
    CHECKMARKS = &H00000008
    DATA       = &H00000020
    FTYPE      = &H00000100
    ID     = &H00000002
    STATE      = &H00000001
    [STRING]   = &H00000040
    SUBMENU    = &H00000004
    TYPE       = &H00000010
End Enum
```
