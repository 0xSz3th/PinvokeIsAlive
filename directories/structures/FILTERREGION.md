
## C# Definition:
```cs
struct FILTERREGION {
   public int idChunk;
   public int cwcStart;
   public int cwcExtent;
}
```

## VB Definition:
```cs
'''  <summary>
  '''   The FILTERREGION structure describes the position and extent
  '''   of a specified portion of text within an object. This 
  '''   structure is used by the IFilter::BindRegion method.
  '''  </summary>
  <StructLayout(LayoutKind.Sequential)> _
  Public Structure FILTERREGION
    '  <summary>
    '   Chunk ID.
    '  </summary>
    Public idChunk As UInt32

    '  <summary>
    '   Beginning of the region, specified as an offset from the beginning of the chunk.
    '  </summary>
    Public cwcStart As UInt32

    '  <summary>
    '   Extent of the region, specified as a number of Unicode characters.
    '  </summary>
    Public cwcExtent As UInt32
  End Structure
```
