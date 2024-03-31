
## C# Definition:
```cs
[Flags]
enum SendMessageTimeoutFlags : uint
{
    SMTO_NORMAL             = 0x0,
    SMTO_BLOCK              = 0x1,
    SMTO_ABORTIFHUNG        = 0x2,
    SMTO_NOTIMEOUTIFNOTHUNG = 0x8,
    SMTO_ERRORONEXIT = 0x20
}
```

## VB.Net Definition:
```cs
<Flags()> _
Public Enum SendMessageTimeoutFlags
    SMTO_NORMAL             = 0
    SMTO_BLOCK              = 1
    SMTO_ABORTIFHUNG        = 2
    SMTO_NOTIMEOUTIFNOTHUNG = 8
    SMTO_ERRORONEXIT = 32
End Enum
```
