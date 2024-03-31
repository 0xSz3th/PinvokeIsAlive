
## C# Definition:
```cs
[Flags]
public enum SnapshotFlags : uint
{
    HeapList = 0x00000001,
    Process  = 0x00000002,
    Thread   = 0x00000004,
    Module   = 0x00000008,
    Module32 = 0x00000010,
    All      = (HeapList | Process | Thread | Module),
    Inherit  = 0x80000000,
    NoHeaps = 0x40000000

}
```

## VB.NET Definition:
```cs
<Flags()> _
Public Enum SnapshotFlags As Integer
    HeapList = &H1
    Process = &H2
    Thread = &H4
    [Module] = &H8
    Module32 = &H10
    Inherit = &H80000000
    All = &Hf
    NoHeaps = &H40000000
End Enum
```
