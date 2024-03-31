
## C# Definition:
```cs
enum CHUNKSTATE {
        /// <summary>
        /// The current chunk is a text-type property.
        /// </summary>
        CHUNK_TEXT = 0x1,
        /// <summary>
        /// The current chunk is a value-type property. 
        /// </summary>
        CHUNK_VALUE = 0x2,
        /// <summary>
        /// Reserved
        /// </summary>
        CHUNK_FILTER_OWNED_VALUE = 0x4
}
```

## VB Definition:
```cs
Enum CHUNKSTATE
        ''' <summary>
        ''' The current chunk is a text-type property.
        ''' </summary>
        CHUNK_TEXT = &H1,
        ''' <summary>
        ''' The current chunk is a value-type property. 
        ''' </summary>
        CHUNK_VALUE = &H2,
        ''' <summary>
        ''' Reserved
        ''' </summary>
        CHUNK_FILTER_OWNED_VALUE = &H4
End Enum
```
