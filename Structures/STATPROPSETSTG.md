
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct STATPROPSETSTG
    {
    /// <summary>
    /// FMTID (GUID) of the current property set, specified when the property set was initially created.
    /// </summary>
    public Guid fmtid;
    /// <summary>
    /// CLSID (GUID) associated with this property set, specified when the property set was initially created
    /// and possibly modified thereafter with IWiaPropertyStorage.SetClass. If not set, the value
    /// will be Guid.Empty.
    /// </summary>
    public Guid clsid;
    /// <summary>
    /// Flag values of the property set, as specified in IWiaPropertySetStorage.Create.
    /// </summary>
    public uint grfFlags;
    /// <summary>
    /// Time in Universal Coordinated Time (UTC) when the property set was last modified.
    /// </summary>
    public FILETIME mtime;
    /// <summary>
    /// Time in UTC when this property set was created.
    /// </summary>
    public FILETIME ctime;
    /// <summary>
    /// Time in UTC when this property set was last accessed.
    /// </summary>
    public FILETIME atime;
    }
```

## VB Definition:
```cs
Structure STATPROPSETSTG 
   Public TODO
End Structure
```
