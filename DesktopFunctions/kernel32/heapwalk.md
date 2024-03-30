
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
static extern bool HeapWalk(IntPtr hHeap, ref PROCESS_HEAP_ENTRY lpEntry);
```

## VB Signature:
```cs
Declare Function heapwalk Lib "kernel32.dll" (TODO) As TODO
```

## User-Defined Types:
```cs
[Flags]
public enum PROCESS_HEAP_ENTRY_WFLAGS : ushort
{
    PROCESS_HEAP_ENTRY_BUSY = 0x0004,
    PROCESS_HEAP_ENTRY_DDESHARE = 0x0020,
    PROCESS_HEAP_ENTRY_MOVEABLE = 0x0010,
    PROCESS_HEAP_REGION = 0x0001,
    PROCESS_HEAP_UNCOMMITTED_RANGE = 0x0002,
}
[StructLayoutAttribute(LayoutKind.Explicit)]
public struct UNION_BLOCK
{
    [FieldOffset(0)]
    public STRUCT_BLOCK Block;

    [FieldOffset(0)]
    public STRUCT_REGION Region;
}
[StructLayoutAttribute(LayoutKind.Sequential)]
public struct STRUCT_BLOCK
{
    public IntPtr hMem;
    public uint dwReserved1_1;
    public uint dwReserved1_2;
    public uint dwReserved1_3;
}
[StructLayoutAttribute(LayoutKind.Sequential)]
public struct STRUCT_REGION
{
    public uint dwCommittedSize;
    public uint dwUnCommittedSize;
    public IntPtr lpFirstBlock;
    public IntPtr lpLastBlock;
}
[StructLayoutAttribute(LayoutKind.Sequential)]
public struct PROCESS_HEAP_ENTRY
{
    public IntPtr lpData;
    public uint cbData;
    public byte cbOverhead;
    public byte iRegionIndex;
    public PROCESS_HEAP_ENTRY_WFLAGS wFlags;
    public UNION_BLOCK UnionBlock;
}
```

## Sample Code:
```cs
PROCESS_HEAP_ENTRY h = new PROCESS_HEAP_ENTRY();
uint size = 0;
while(HeapWalk(heapHandle, ref h))
{
    if (h.wFlags == PROCESS_HEAP_ENTRY_WFLAGS.PROCESS_HEAP_ENTRY_BUSY)
    {
    size += h.cbData;
    }
}
Console.WriteLine("Size: " + size);
```
