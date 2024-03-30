
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct IMAGE_DATA_DIRECTORY
    {
        public UInt32 VirtualAddress;
        public UInt32 Size;
    }
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential, Pack:=1)> _
  Public Structure IMAGE_DATA_DIRECTORY

    ''' <summary>
    ''' RVA of the data 
    ''' </summary>
    ''' <remarks></remarks>
    Public VirtualAddress As UInt32

    ''' <summary>
    ''' Size of the data
    ''' </summary>
    ''' <remarks></remarks>
    Public Size As UInt32

  End Structure
```

## VB 6 Definition:
```cs
Public Type IMAGE_DATA_DIRECTORY
    VirtualAddress As Long  ' relative virtual address of the table (aka data)
    Size As Long            ' Size of the table (aka data)
  End Type
```
