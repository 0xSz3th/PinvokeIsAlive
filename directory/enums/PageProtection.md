
## C# Definition:
```cs
[Flags]
enum PageProtection : uint {
   NoAccess =     0x01,
   Readonly =     0x02,
   ReadWrite =    0x04,
   WriteCopy =    0x08,
   Execute =      0x10,
   ExecuteRead =      0x20,
   ExecuteReadWrite = 0x40,
   ExecuteWriteCopy = 0x80,
   Guard =        0x100,
   NoCache =      0x200,
   WriteCombine =     0x400,
}
```

## VB Definition:
```cs
<Flags> _
Enum PageProtection
  NoAccess = &H1
  [ReadOnly] = &H2
  ReadWrite = &H4
  WriteCopy = &H8
  Execute = &H10
  ExecuteRead = &H20
  ExecuteReadWrite = &H40
  ExecuteWriteCopy = &H80
  Guard = &H100
  NoCache = &H200
  WriteCombine = &H400
End Enum
```
