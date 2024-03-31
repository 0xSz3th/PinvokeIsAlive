
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct PARTITION_INFORMATION_MBR
{
     [MarshalAs(UnmanagedType.U1)]
     public PARTITION_TYPE PartitionType;
     [MarshalAs(UnmanagedType.U1)]
     public bool BootIndicator;
     [MarshalAs(UnmanagedType.U1)]
     public bool RecognizedPartition;
     public uint HiddenSectors;
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _
Public Structure PARTITION_INFORMATION_MBR
    <MarshalAs(UnmanagedType.U1)> _
    Public PartitionType As PARTITION_TYPE
    <MarshalAs(UnmanagedType.U1)> _
    Public BootIndicator As Boolean
    <MarshalAs(UnmanagedType.U1)> _
    Public RecognizedPartition As Boolean
    Public HiddenSectors As UInteger
End Structure
```
