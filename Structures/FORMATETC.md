
## C# Signature:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct FORMATETC
{
    public short cfFormat;
    public IntPtr ptd;
    [MarshalAs(UnmanagedType.U4)]
    public DVASPECT dwAspect;    
    public int lindex;
    [MarshalAs(UnmanagedType.U4)]
    public TYMED tymed;
    };

    ///// <summary>
    ///// The DVASPECT enumeration values specify the desired data or view aspect of the object when drawing or getting data.
    ///// </summary>
    [Flags]
    public enum DVASPECT
    {
    DVASPECT_CONTENT = 1,
    DVASPECT_THUMBNAIL = 2,
    DVASPECT_ICON = 4,
    DVASPECT_DOCPRINT = 8
    }

    // Summary:
    //     Provides the managed definition of the TYMED structure.
    [Flags]
    public enum TYMED
    {
    // Summary:
    //     No data is being passed.
    TYMED_NULL = 0,
    //
    // Summary:
    //     The storage medium is a global memory handle (HGLOBAL). Allocate the global
    //     handle with the GMEM_SHARE flag. If the System.Runtime.InteropServices.ComTypes.STGMEDIUMSystem.Runtime.InteropServices.ComTypes.STGMEDIUM.pUnkForRelease
    //     member is null, the destination process should use GlobalFree to release
    //     the memory.
    TYMED_HGLOBAL = 1,
    //
    // Summary:
    //     The storage medium is a disk file identified by a path. If the STGMEDIUMSystem.Runtime.InteropServices.ComTypes.STGMEDIUM.pUnkForRelease
    //     member is null, the destination process should use OpenFile to delete the
    //     file.
    TYMED_FILE = 2,
    //
    // Summary:
    //     The storage medium is a stream object identified by an IStream pointer. Use
    //     ISequentialStream::Read to read the data. If the System.Runtime.InteropServices.ComTypes.STGMEDIUMSystem.Runtime.InteropServices.ComTypes.STGMEDIUM.pUnkForRelease
    //     member is not null, the destination process should use IStream::Release to
    //     release the stream component.
    TYMED_ISTREAM = 4,
    //
    // Summary:
    //     The storage medium is a storage component identified by an IStorage pointer.
    //     The data is in the streams and storages contained by this IStorage instance.
    //     If the System.Runtime.InteropServices.ComTypes.STGMEDIUMSystem.Runtime.InteropServices.ComTypes.STGMEDIUM.pUnkForRelease
    //     member is not null, the destination process should use IStorage::Release
    //     to release the storage component.
    TYMED_ISTORAGE = 8,
    //
    // Summary:
    //     The storage medium is a Graphics Device Interface (GDI) component (HBITMAP).
    //     If the System.Runtime.InteropServices.ComTypes.STGMEDIUMSystem.Runtime.InteropServices.ComTypes.STGMEDIUM.pUnkForRelease
    //     member is null, the destination process should use DeleteObject to delete
    //     the bitmap.
    TYMED_GDI = 16,
    //
    // Summary:
    //     The storage medium is a metafile (HMETAFILE). Use the Windows or WIN32 functions
    //     to access the metafile's data. If the System.Runtime.InteropServices.ComTypes.STGMEDIUMSystem.Runtime.InteropServices.ComTypes.STGMEDIUM.pUnkForRelease
    //     member is null, the destination process should use DeleteMetaFile to delete
    //     the bitmap.
    TYMED_MFPICT = 32,
    //
    // Summary:
    //     The storage medium is an enhanced metafile. If the System.Runtime.InteropServices.ComTypes.STGMEDIUMSystem.Runtime.InteropServices.ComTypes.STGMEDIUM.pUnkForRelease
    //     member is null, the destination process should use DeleteEnhMetaFile to delete
    //     the bitmap.
    TYMED_ENHMF = 64,
    }
```

## VB Definition:
```cs
Public cfFormat As Short
    Public ptd As IntPtr
    <MarshalAs(UnmanagedType.U4)> _
    Public dwAspect As DVASPECT
    Public lindex As Integer
    <MarshalAs(UnmanagedType.U4)> _
    Public tymed As TYMED
```

## VB Definition:
```cs
DVASPECT_CONTENT = 1
    DVASPECT_THUMBNAIL = 2
    DVASPECT_ICON = 4
    DVASPECT_DOCPRINT = 8
```

## VB Definition:
```cs
' Summary:
    '     No data is being passed.
    TYMED_NULL = 0
    '
    ' Summary:
    '     The storage medium is a global memory handle (HGLOBAL). Allocate the global
    '     handle with the GMEM_SHARE flag. If the System.Runtime.InteropServices.ComTypes.STGMEDIUMSystem.Runtime.InteropServices.ComTypes.STGMEDIUM.pUnkForRelease
    '     member is null, the destination process should use GlobalFree to release
    '     the memory.
    TYMED_HGLOBAL = 1
    '
    ' Summary:
    '     The storage medium is a disk file identified by a path. If the STGMEDIUMSystem.Runtime.InteropServices.ComTypes.STGMEDIUM.pUnkForRelease
    '     member is null, the destination process should use OpenFile to delete the
    '     file.
    TYMED_FILE = 2
    '
    ' Summary:
    '     The storage medium is a stream object identified by an IStream pointer. Use
    '     ISequentialStream::Read to read the data. If the System.Runtime.InteropServices.ComTypes.STGMEDIUMSystem.Runtime.InteropServices.ComTypes.STGMEDIUM.pUnkForRelease
    '     member is not null, the destination process should use IStream::Release to
    '     release the stream component.
    TYMED_ISTREAM = 4
    '
    ' Summary:
    '     The storage medium is a storage component identified by an IStorage pointer.
    '     The data is in the streams and storages contained by this IStorage instance.
    '     If the System.Runtime.InteropServices.ComTypes.STGMEDIUMSystem.Runtime.InteropServices.ComTypes.STGMEDIUM.pUnkForRelease
    '     member is not null, the destination process should use IStorage::Release
    '     to release the storage component.
    TYMED_ISTORAGE = 8
    '
    ' Summary:
    '     The storage medium is a Graphics Device Interface (GDI) component (HBITMAP).
    '     If the System.Runtime.InteropServices.ComTypes.STGMEDIUMSystem.Runtime.InteropServices.ComTypes.STGMEDIUM.pUnkForRelease
    '     member is null, the destination process should use DeleteObject to delete
    '     the bitmap.
    TYMED_GDI = 16
    '
    ' Summary:
    '     The storage medium is a metafile (HMETAFILE). Use the Windows or WIN32 functions
    '     to access the metafile's data. If the System.Runtime.InteropServices.ComTypes.STGMEDIUMSystem.Runtime.InteropServices.ComTypes.STGMEDIUM.pUnkForRelease
    '     member is null, the destination process should use DeleteMetaFile to delete
    '     the bitmap.
    TYMED_MFPICT = 32
    '
    ' Summary:
    '     The storage medium is an enhanced metafile. If the System.Runtime.InteropServices.ComTypes.STGMEDIUMSystem.Runtime.InteropServices.ComTypes.STGMEDIUM.pUnkForRelease
    '     member is null, the destination process should use DeleteEnhMetaFile to delete
    '     the bitmap.
    TYMED_ENHMF = 64
```
