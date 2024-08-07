
## C# Definition:
```cs
[ComImport, Guid("89BCB740-6119-101A-BCB7-00DD010655AF")]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
interface IFilter
{
   /// <summary>
   /// The IFilter::Init method initializes a filtering session.
   /// </summary>
   [PreserveSig]
   IFilterReturnCodes Init(
     //[in] Flag settings from the IFILTER_INIT enumeration for
     // controlling text standardization, property output, embedding
     // scope, and IFilter access patterns. 
     IFILTER_INIT grfFlags,

     // [in] The size of the attributes array. When nonzero, cAttributes
     //  takes 
     // precedence over attributes specified in grfFlags. If no
     // attribute flags 
     // are specified and cAttributes is zero, the default is given by
     // the 
     // PSGUID_STORAGE storage property set, which contains the date and
     //  time 
     // of the last write to the file, size, and so on; and by the
     //  PID_STG_CONTENTS 
     // 'contents' property, which maps to the main contents of the
     // file. 
     // For more information about properties and property sets, see
     // Property Sets. 
     int cAttributes,

     //[in] Array of pointers to FULLPROPSPEC structures for the
     // requested properties. 
     // When cAttributes is nonzero, only the properties in aAttributes
     // are returned. 
     IntPtr aAttributes,

     // [out] Information about additional properties available to the
     //  caller; from the IFILTER_FLAGS enumeration. 
     out IFILTER_FLAGS pdwFlags);

   /// <summary>
   /// The IFilter::GetChunk method positions the filter at the beginning
   /// of the next chunk, 
   /// or at the first chunk if this is the first call to the GetChunk
   /// method, and returns a description of the current chunk. 
   /// </summary>
   [PreserveSig]
   IFilterReturnCodes GetChunk(out STAT_CHUNK pStat);

   /// <summary>
   /// The IFilter::GetText method retrieves text (text-type properties)
   /// from the current chunk, 
   /// which must have a CHUNKSTATE enumeration value of CHUNK_TEXT.
   /// </summary>
   [PreserveSig]
   IFilterReturnCodes GetText(
       // [in/out] On entry, the size of awcBuffer array in wide/Unicode
       // characters. On exit, the number of Unicode characters written to
       // awcBuffer. 
       // Note that this value is not the number of bytes in the buffer. 
       ref int pcwcBuffer,

       // Text retrieved from the current chunk. Do not terminate the
       // buffer with a character.  
       [Out(), MarshalAs(UnmanagedType.LPWStr)] 
       StringBuilder awcBuffer);

   /// <summary>
   /// The IFilter::GetValue method retrieves a value (public
   /// value-type property) from a chunk, 
   /// which must have a CHUNKSTATE enumeration value of CHUNK_VALUE.
   /// </summary>
   [PreserveSig]
   IFilterReturnCodes GetValue(
       // Allocate the PROPVARIANT structure with CoTaskMemAlloc. Some
       // PROPVARIANT 
       // structures contain pointers, which can be freed by calling the
       // PropVariantClear function. 
       // It is up to the caller of the GetValue method to call the
       //   PropVariantClear method.            
       // ref IntPtr ppPropValue
       // [MarshalAs(UnmanagedType.Struct)]
       ref IntPtr PropVal);

   /// <summary>
   /// The IFilter::BindRegion method retrieves an interface representing
   /// the specified portion of the object. 
   /// Currently reserved for future use.
   /// </summary>
   [PreserveSig]
   IFilterReturnCodes BindRegion(ref FILTERREGION origPos,
     ref Guid riid, ref object ppunk);
}
```

## VB Definition:
```cs
<ComImport, Guid("89BCB740-6119-101A-BCB7-00DD010655AF")> _
<InterfaceType(ComInterfaceType.InterfaceIsIUnknown)>
Public Interface IFilter 
      ''' <summary>
      '''   The IFilter::Init method initializes a filtering session.
      ''' </summary>
   <PreserveSig> _
   Function Init( _
        ByVal grfFlags As IFILTER_INIT, _
        ByVal cAttributes As Integer , _
        ByVal aAttributes As IntPtr, _
        ByVal pdwFlags As IFILTER_FLAGS _
        ) As IFilterReturnCodes
        ' <in> grfFlags - Flag settings from the IFILTER_INIT enumeration for
        ' controlling text standardization, property output, embedding
        ' scope, and IFilter access patterns.
        ' <in> cAttributes - The size of the attributes array. When nonzero, cAttributes
        ' takes 
        ' precedence over attributes specified in grfFlags. If no
        ' attribute flags are specified and cAttributes is zero, the default is 
        ' given by the  PSGUID_STORAGE storage property set, which contains the
        ' date and time of the last write to the file, size, and so on; and by 
        ' the PID_STG_CONTENTS 'contents' property, which maps to the main contents
        ' of the file. 
        ' For more information about properties and property sets, see
        ' Property Sets.
        '<in> aAttributes - Array of pointers to FULLPROPSPEC structures for the
        ' requested properties. 
        ' When cAttributes is nonzero, only the properties in aAttributes
        ' are returned. 
        ' <out> pdwFlags - Information about additional properties available to the
        '  caller; from the IFILTER_FLAGS enumeration.

      '///////////////////////////////////////
     ''' <summary>
     '''    The IFilter::GetChunk method positions the filter at the beginning
     '''    of the next chunk, 
     '''    or at the first chunk if this is the first call to the GetChunk
     '''    method, and returns a description of the current chunk. 
     ''' </summary>
   <PreserveSig> _
   Function GetChunk( _
       ByVal pStat As STAT_CHUNK _
            ) As IFilterReturnCodes 

      '///////////////////////////////////////

     ''' <summary>
     '''   The IFilter::GetText method retrieves text (text-type properties)
     '''   from the current chunk, 
     '''   which must have a CHUNKSTATE enumeration value of CHUNK_TEXT.
     ''' </summary>
   <PreserveSig> _
   Function GetText( _
        ByRef pcwcBuffer As Integer, _
        <MarshalAs(UnmanagedType.LPWStr)> _
           awcBuffer As StringBuilderByVal _
      ) As IFilterReturnCodes 
     ' <in/out> pcwcBuffer - On entry, the size of awcBuffer array in wide/Unicode
     ' characters. On exit, the number of Unicode characters written to
     ' awcBuffer. 
     ' Note that this value is not the number of bytes in the buffer. 
     ' Text retrieved from the current chunk. Do not terminate the
     ' buffer with a character.

      '///////////////////////////////////////

     ''' <summary>
     '''   The IFilter::GetValue method retrieves a value (public
     '''   value-type property) from a chunk, 
     '''   which must have a CHUNKSTATE enumeration value of CHUNK_VALUE.
     ''' </summary>
   <PreserveSig> _
   Function GetValue( _
              ByRef PropVal As IntPtr _
            ) As IFilterReturnCodes
    ' Allocate the PROPVARIANT structure with CoTaskMemAlloc. Some
    ' PROPVARIANT 
    ' structures contain pointers, which can be freed by calling the
    ' PropVariantClear function. 
    ' It is up to the caller of the GetValue method to call the
    '   PropVariantClear method.
    ' <MarshalAs(UnmanagedType.Struct)> _
    '    ByRef ppPropValue As IntPtr 

      '///////////////////////////////////////

     ''' <summary>
     '''   The IFilter::BindRegion method retrieves an interface representing
     '''   the specified portion of the object. 
     '''   Currently reserved for future use.
     ''' </summary>
   <PreserveSig> _
   Function BindRegion( _
               ByRef origPos As FILTERREGION, _
               ByRef riid As Guid, _
               ByRef ppunk As object _
              ) As IFilterReturnCodes

End Interface
```
