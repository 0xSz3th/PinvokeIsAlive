
## C# Definition:
```cs
[Flags]
public enum STGM : int
{
    DIRECT        = 0x00000000,
    TRANSACTED    = 0x00010000,
    SIMPLE        = 0x08000000,
    READ        = 0x00000000,
    WRITE        = 0x00000001,
    READWRITE        = 0x00000002,
    SHARE_DENY_NONE    = 0x00000040,
    SHARE_DENY_READ    = 0x00000030,
    SHARE_DENY_WRITE    = 0x00000020,
    SHARE_EXCLUSIVE    = 0x00000010,
    PRIORITY        = 0x00040000,
    DELETEONRELEASE    = 0x04000000,
    NOSCRATCH        = 0x00100000,
    CREATE        = 0x00001000,
    CONVERT        = 0x00020000,
    FAILIFTHERE    = 0x00000000,
    NOSNAPSHOT    = 0x00200000,
    DIRECT_SWMR    = 0x00400000,
}
```

## VB Definition:
```cs
<Flags()> _
Enum STGM
    DIRECT        = 0
    TRANSACTED    = 65536
    SIMPLE        = 134217728
    READ        = 0
    WRITE        = 1
    READWRITE        = 2
    SHARE_DENY_NONE    = 64
    SHARE_DENY_READ    = 48
    SHARE_DENY_WRITE    = 32
    SHARE_EXCLUSIVE    = 16
    PRIORITY        = 262144
    DELETEONRELEASE    = 67108864
    NOSCRATCH        = 1048576
    CREATE        = 4096
    CONVERT        = 131072
    FAILIFTHERE    = 0
    NOSNAPSHOT    = 2097152
    DIRECT_SWMR    = 4194304
End Enum
```
