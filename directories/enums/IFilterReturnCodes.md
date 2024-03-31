
## C# Definition:
```cs
enum IFilterReturnCodes : uint {
        /// <summary>
        /// Success
        /// </summary>
        S_OK = 0,
        /// <summary>
        /// The function was denied access to the filter file. 
        /// </summary>
        E_ACCESSDENIED = 0x80070005,
        /// <summary>
        /// The function encountered an invalid handle,
        /// probably due to a low-memory situation. 
        /// </summary>
        E_HANDLE = 0x80070006,
        /// <summary>
        /// The function received an invalid parameter.
        /// </summary>
        E_INVALIDARG = 0x80070057,
        /// <summary>
        /// Out of memory
        /// </summary>
        E_OUTOFMEMORY = 0x8007000E,
        /// <summary>
        /// Not implemented
        /// </summary>
        E_NOTIMPL = 0x80004001,
        /// <summary>
        /// Unknown error
        /// </summary>
        E_FAIL = 0x80000008,
        /// <summary>
        /// File not filtered due to password protection
        /// </summary>
        FILTER_E_PASSWORD = 0x8004170B,
        /// <summary>
        /// The document format is not recognised by the filter
        /// </summary>
        FILTER_E_UNKNOWNFORMAT = 0x8004170C,
        /// <summary>
        /// No text in current chunk
        /// </summary>
        FILTER_E_NO_TEXT = 0x80041705,
        /// <summary>
        /// No values in current chunk
        /// </summary>
        FILTER_E_NO_VALUES = 0x80041706,
        /// <summary>
        /// No more chunks of text available in object
        /// </summary>
        FILTER_E_END_OF_CHUNKS = 0x80041700,
        /// <summary>
        /// No more text available in chunk
        /// </summary>
        FILTER_E_NO_MORE_TEXT = 0x80041701,
        /// <summary>
        /// No more property values available in chunk
        /// </summary>
        FILTER_E_NO_MORE_VALUES = 0x80041702,
        /// <summary>
        /// Unable to access object
        /// </summary>
        FILTER_E_ACCESS = 0x80041703,
        /// <summary>
        /// Moniker doesn't cover entire region
        /// </summary>
        FILTER_W_MONIKER_CLIPPED = 0x00041704,
        /// <summary>
        /// Unable to bind IFilter for embedded object
        /// </summary>
        FILTER_E_EMBEDDING_UNAVAILABLE = 0x80041707,
        /// <summary>
        /// Unable to bind IFilter for linked object
        /// </summary>
        FILTER_E_LINK_UNAVAILABLE = 0x80041708,
        /// <summary>
        ///  This is the last text in the current chunk
        /// </summary>
        FILTER_S_LAST_TEXT = 0x00041709,
        /// <summary>
        /// This is the last value in the current chunk
        /// </summary>
        FILTER_S_LAST_VALUES = 0x0004170A
}
```

## VB Definition:
```cs
Public Enum IFilterReturnCodes
    S_OK = 0
    E_ACCESSDENIED = &H80070005
    E_HANDLE = &H80070006
    E_INVALIDARG = &H80070057
    E_OUTOFMEMORY = &H8007000E
    E_NOTIMPL = &H80004001
    E_FAIL = &H80000008
    FILTER_E_PASSWORD = &H8004170B
    FILTER_E_UNKNOWNFORMAT = &H8004170C
    FILTER_E_NO_TEXT = &H80041705
    FILTER_E_NO_VALUES = &H80041706
    FILTER_E_END_OF_CHUNKS = &H80041700
    FILTER_E_NO_MORE_TEXT = &H80041701
    FILTER_E_NO_MORE_VALUES = &H80041702
    FILTER_E_ACCESS = &H80041703
    FILTER_W_MONIKER_CLIPPED = &H41704
    FILTER_E_EMBEDDING_UNAVAILABLE = &H80041707
    FILTER_E_LINK_UNAVAILABLE = &H80041708
    FILTER_S_LAST_TEXT = &H41709
    FILTER_S_LAST_VALUES = &H4170A
    End Enum
```
