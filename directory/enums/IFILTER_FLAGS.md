
## C# Definition:
```cs
[Flags]
enum IFILTER_FLAGS {
   /// <summary>
   /// The caller should use the IPropertySetStorage and IPropertyStorage
   /// interfaces to locate additional properties. 
   /// When this flag is set, properties available through COM
   /// enumerators should not be returned from IFilter. 
   /// </summary>
   IFILTER_FLAGS_OLE_PROPERTIES = 1
}
```

## VB Definition:
```cs
<Flags()> _
   Public Enum IFILTER_FLAGS
     '// The caller should use the IPropertySetStorage and IPropertyStorage interfaces
     '// to locate additional properties. When this flag is set, properties 
     '// available through COM enumerators should not be returned from IFilter.
     IFILTER_FLAGS_OLE_PROPERTIES = 1
   End Enum
```
