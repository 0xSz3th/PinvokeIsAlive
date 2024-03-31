
## C# Definition:
```cs
/// <summary>
/// Enumerates the different breaking types that occur between 
/// chunks of text read out by the FileFilter.
/// </summary>
enum CHUNK_BREAKTYPE
{
        /// <summary>
        /// No break is placed between the current chunk and the previous chunk.
        /// The chunks are glued together. 
        /// </summary>
        CHUNK_NO_BREAK = 0,
        /// <summary>
        /// A word break is placed between this chunk and the previous chunk that
        /// had the same attribute. 
        /// Use of CHUNK_EOW should be minimized because the choice of word
        /// breaks is language-dependent, 
        /// so determining word breaks is best left to the search engine. 
        /// </summary>
        CHUNK_EOW = 1,
        /// <summary>
        /// A sentence break is placed between this chunk and the previous chunk
        /// that had the same attribute. 
        /// </summary>
        CHUNK_EOS = 2,
        /// <summary>
        /// A paragraph break is placed between this chunk and the previous chunk
        /// that had the same attribute.
        /// </summary>     
        CHUNK_EOP = 3,
        /// <summary>
        /// A chapter break is placed between this chunk and the previous chunk
        /// that had the same attribute. 
        /// </summary>
        CHUNK_EOC = 4
}
```

## VB Definition:
```cs
''' <summary>
  '''   Enumerates the different breaking types that occur between 
  '''   chunks of text read out by the FileFilter.
  ''' </summary>
  Public Enum CHUNK_BREAKTYPE
    '  <summary>
    '    No break is placed between the current chunk and the previous chunk.
    '    The chunks are glued together. 
    '  </summary>
    CHUNK_NO_BREAK = 0

    '  <summary>
    '    A word break is placed between this chunk and the previous chunk that
    '    had the same attribute. 
    '    Use of CHUNK_EOW should be minimized because the choice of word
    '    breaks is language-dependent 
    '    so determining word breaks is best left to the search engine. 
    '  </summary>
    CHUNK_EOW = 1

    '  <summary>
    '    A sentence break is placed between this chunk and the previous chunk
    '    that had the same attribute. 
    '  </summary>
    CHUNK_EOS = 2

    '  <summary>
    '    A paragraph break is placed between this chunk and the previous chunk
    '    that had the same attribute.
    '  </summary>     
    CHUNK_EOP = 3

    '  <summary>
    '    A chapter break is placed between this chunk and the previous chunk
    '    that had the same attribute. 
    '  </summary>
    CHUNK_EOC = 4
  End Enum
```
