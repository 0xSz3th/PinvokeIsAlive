
## C# Signature:
```cs
/// <summary>
    /// The StgCreateDocfileOnILockBytes function creates and opens a new compound file 
    /// storage object on top of a byte-array object provided by the caller. The storage 
    /// object supports the COM-provided, compound-file implementation for the IStorage interface.
    /// </summary>
    /// <param name="plkbyt">A pointer to the ILockBytes interface on the underlying byte-array object on which to create a compound file.</param>
    /// <param name="grfMode">Specifies the access mode to use when opening the new compound file. For more information, see STGM Constants.</param>
    /// <param name="reserved">Reserved for future use; must be zero.</param>
    /// <param name="ppstgOpen">A pointer to the location of the IStorage pointer on the new storage object.</param>
    /// <returns>
    /// S_OK
    ///    Indicates that the compound file was successfully created.
    ///STG_E_ACCESSDENIED
    ///    Access denied because the caller does not have enough permissions, or another caller has the file open and locked.
    ///STG_E_FILEALREADYEXISTS
    ///    Indicates that the compound file already exists and the grfMode parameter is set to STGM_FAILIFTHERE.
    ///STG_E_INSUFFICIENTMEMORY
    ///    Indicates that the storage object was not created due to inadequate memory.
    ///STG_E_INVALIDPOINTER
    ///    Indicates that a non-valid pointer was in the pLkbyt parameter or the ppStgOpen parameter.
    ///STG_E_INVALIDFLAG
    ///    Indicates that a non-valid flag combination was in the grfMode parameter.
    ///STG_E_TOOMANYOPENFILES
    ///    Indicates that the storage object was not created due to a lack of file handles.
    ///STG_E_LOCKVIOLATION
    ///    Access denied because another caller has the file open and locked.
    ///STG_E_SHAREVIOLATION
    ///    Access denied because another caller has the file open and locked.
    ///STG_S_CONVERTED
    ///    Indicates that the compound file was successfully converted. The original byte-array object was successfully converted to IStorage format.
    /// </returns>
    [DllImport ("ole32.dll")]
    public extern static int StgCreateDocfileOnILockBytes(ILockBytes plkbyt, StgmConstants grfMode, int reserved, out IStorage ppstgOpen);
```
