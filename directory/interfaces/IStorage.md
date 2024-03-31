
## C# Definition:
```cs
[ComImport]
[Guid("0000000b-0000-0000-C000-000000000046")]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
interface IStorage {
    void CreateStream( 
        /* [string][in] */ string pwcsName,
        /* [in] */ uint grfMode,
        /* [in] */ uint reserved1,
        /* [in] */ uint reserved2,
        /* [out] */ out IStream ppstm);

    void OpenStream( 
        /* [string][in] */ string pwcsName,
        /* [unique][in] */ IntPtr reserved1,
        /* [in] */ uint grfMode,
        /* [in] */ uint reserved2,
        /* [out] */ out IStream ppstm);

    void CreateStorage( 
        /* [string][in] */ string pwcsName,
        /* [in] */ uint grfMode,
        /* [in] */ uint reserved1,
        /* [in] */ uint reserved2,
        /* [out] */ out IStorage ppstg);

    void OpenStorage( 
        /* [string][unique][in] */ string pwcsName,
        /* [unique][in] */ IStorage pstgPriority,
        /* [in] */ uint grfMode,
        /* [unique][in] */ IntPtr snbExclude,
        /* [in] */ uint reserved,
        /* [out] */ out IStorage ppstg);

    void CopyTo( 
        /* [in] */ uint ciidExclude,
        /* [size_is][unique][in] */ [In, MarshalAs(UnmanagedType.LPArray, SizeParamIndex=0)] Guid[] rgiidExclude,
        /* [unique][in] */ IntPtr snbExclude,
        /* [unique][in] */ IStorage pstgDest);

    void MoveElementTo( 
        /* [string][in] */ string pwcsName,
        /* [unique][in] */ IStorage pstgDest,
        /* [string][in] */ string pwcsNewName,
        /* [in] */ uint grfFlags);

    void Commit( 
        /* [in] */ uint grfCommitFlags);

    void Revert();

    void EnumElements( 
        /* [in] */ uint reserved1,
        /* [size_is][unique][in] */ IntPtr reserved2,
        /* [in] */ uint reserved3,
        /* [out] */ out IEnumSTATSTG ppenum);

    void DestroyElement( 
        /* [string][in] */ string pwcsName);

    void RenameElement( 
        /* [string][in] */ string pwcsOldName,
        /* [string][in] */ string pwcsNewName);

    void SetElementTimes( 
        /* [string][unique][in] */ string pwcsName,
        /* [unique][in] */ FILETIME pctime,
        /* [unique][in] */ FILETIME patime,
        /* [unique][in] */ FILETIME pmtime);

    void SetClass( 
        /* [in] */ Guid clsid);

    void SetStateBits( 
        /* [in] */ uint grfStateBits,
        /* [in] */ uint grfMask);

    void Stat( 
        /* [out] */ out STATSTG pstatstg,
        /* [in] */ uint grfStatFlag);

}
```

## VB.Net Definition:
```cs
<ComImportAttribute(),  _
Guid("0000000b-0000-0000-c000-000000000046"),  _
InterfaceType(ComInterfaceType.InterfaceIsIUnknown)>  _
Interface IStorage
    Sub CreateStream(ByVal pwcsName As String,
                     ByVal grfMode As UInteger,
                     ByVal reserved1 As UInteger,
                     ByVal reserved2 As UInteger,
                     ByRef ppstm As IStream)

    Sub OpenStream(ByVal pwcsName As String,
                   ByVal reserved1 As IntPtr,
                   ByVal grfMode As UInteger,
                   ByVal reserved2 As UInteger,
                   ByRef ppstm As IStream)

    Sub CreateStorage(ByVal pwcsName As String,
                      ByVal grfMode As UInteger,
                      ByVal reserved1 As UInteger,
                      ByVal reserved2 As UInteger,
                      ByRef ppstg As IStorage)

    Sub OpenStorage(ByVal pwcsName As String,
                    ByVal pstgPriority As IStorage,
                    ByVal grfMode As UInteger,
                    ByVal snbExclude As IntPtr,
                    ByVal reserved As UInteger,
                    ByRef ppstg As IStorage)

    Sub CopyTo(ByVal ciidExclude As UInteger,
               ByVal rgiidExclude() As Guid,
               ByVal snbExclude As IntPtr,
               ByVal pstgDest As IStorage)

    Sub MoveElementTo(ByVal pwcsName As String,
                      ByVal pstgDest As IStorage,
                      ByVal pwcsNewName As String,
                      ByVal grfFlags As UInteger)

    Sub Commit(ByVal grfCommitFlags As UInteger)

    Sub Revert()

    Sub EnumElements(ByVal reserved1 As UInteger,
                     ByVal reserved2 As IntPtr,
                     ByVal reserved3 As UInteger,
                     ByRef ppenum As IEnumSTATSTG)

    Sub DestroyElement(ByVal pwcsName As String)

    Sub RenameElement(ByVal pwcsOldName As String,
                      ByVal pwcsNewName As String)

    Sub SetElementTimes(ByVal pwcsName As String,
                        ByVal pctime As FILETIME,
                        ByVal patime As FILETIME,
                        ByVal pmtime As FILETIME)

    Sub SetClass(ByVal clsid As Guid)

    Sub SetStateBits(ByVal grfStateBits As UInteger,
                     ByVal grfMask As UInteger)

    Sub Stat(ByRef pstatstg As STATSTG,
             ByVal grfStatFlag As UInteger)
End Interface
```
