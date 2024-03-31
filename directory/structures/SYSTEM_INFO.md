
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct SYSTEM_INFO
{
    public ushort processorArchitecture;
    ushort reserved;
    public uint pageSize;
    public IntPtr minimumApplicationAddress;
    public IntPtr maximumApplicationAddress;
    public IntPtr activeProcessorMask;
    public uint numberOfProcessors;
    public uint processorType;
    public uint allocationGranularity;
    public ushort processorLevel;
    public ushort processorRevision;
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _
Public Structure SYSTEM_INFO
    Dim wProcessorArchitecture As Int16
    Dim wReserved As Int16
    Dim dwPageSize As Integer
    Dim lpMinimumApplicationAddress As Integer
    Dim lpMaximumApplicationAddress As Integer
    Dim dwActiveProcessorMask As Integer
    Dim dwNumberOfProcessors As Integer
    Dim dwProcessorType As Integer
    Dim dwAllocationGranularity As Integer
    Dim wProcessorLevel As Int16
    Dim wProcessorRevision As Int16
End Structure
```
