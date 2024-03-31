
## C# Definition:
```cs
[Flags]
enum MoveFileFlags
{
    MOVEFILE_REPLACE_EXISTING           = 0x00000001,
    MOVEFILE_COPY_ALLOWED               = 0x00000002,
    MOVEFILE_DELAY_UNTIL_REBOOT         = 0x00000004,
    MOVEFILE_WRITE_THROUGH              = 0x00000008,
    MOVEFILE_CREATE_HARDLINK            = 0x00000010,
    MOVEFILE_FAIL_IF_NOT_TRACKABLE      = 0x00000020
}
```

## VB.Net Definition:
```cs
Enum MoveFileFlags As UInteger
    MOVEFILE_REPLACE_EXISTING           = &H1
    MOVEFILE_COPY_ALLOWED               = &H2
    MOVEFILE_DELAY_UNTIL_REBOOT         = &H4
    MOVEFILE_WRITE_THROUGH              = &H8
    MOVEFILE_CREATE_HARDLINK            = &H10
    MOVEFILE_FAIL_IF_NOT_TRACKABLE      = &H20
End Enum
```
