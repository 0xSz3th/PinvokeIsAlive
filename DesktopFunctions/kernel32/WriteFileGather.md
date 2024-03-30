
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool WriteFileGather(IntPtr hFile, [Out] FILE_SEGMENT_ELEMENT []
   aSegmentArray, uint nNumberOfBytesToWrite, IntPtr lpReserved,
   [In] ref System.Threading.NativeOverlapped lpOverlapped);
```

## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true)]
static extern unsafe int WriteFileGather(IntPtr hFile, 
  FILE_SEGMENT_ELEMENT* aSegmentArray, int nNumberOfBytesToWrite, 
  IntPtr lpReserved, System.Threading.NativeOverlapped* lpOverlapped);
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Explicit, Size = 8)]
internal struct FILE_SEGMENT_ELEMENT
{
  [FieldOffset(0)]
  public IntPtr Buffer;
  [FieldOffset(0)]
  public UInt64 Alignment;
}
```

## Sample Code:
```cs
// Prepares the array of file segments given an IntPtr[] ABuffers (only uses ACount of the buffers so that these arrays can be pooled)
// The size of each buffer (ASize) must be a multiple of the system's page size (get using GetSystemInfo)
int LPerBufferPageCount = ASize / FPageSize;
FILE_SEGMENT_ELEMENT* LElements = stackalloc FILE_SEGMENT_ELEMENT[(ACount * LPerBufferPageCount) + 1];
for (int LElementIndex = 0; LElementIndex < ACount; LElementIndex++)
{
  for (int LPageIndex = 0; LPageIndex < LPerBufferPageCount; LPageIndex++)
   LElements[(LElementIndex * LPerBufferPageCount) + LPageIndex].Buffer = 
    (IntPtr)((uint)ABuffers[LElementIndex] + (LPageIndex * FPageSize));
}
LElements[(ACount * LPerBufferPageCount)].Buffer = IntPtr.Zero;
```
