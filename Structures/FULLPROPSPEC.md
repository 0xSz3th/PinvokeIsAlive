
## C# Definition:
```cs
struct FULLPROPSPEC {
   public Guid guidPropSet;
   public PROPSPEC psProperty;
}
```

## VB Definition:
```cs
''' <summary>
  '''   The FULLPROPSPEC structure specifies a property set and a property within the property set.
  ''' </summary>
  <StructLayout(LayoutKind.Sequential)> _
  Public Structure FULLPROPSPEC
    '  <summary>
    '    The globally unique identifier (GUID) that identifies the property set.
    '  </summary>
    Public guidPropSet As Guid

    '  <summary>
    '    Pointer to the PROPSPEC structure that specifies a property either by its
    '    property identifier (propid) or by the associated string name (lpwstr).
    '  </summary>
    Public psProperty As PROPSPEC
  End Structure
```
