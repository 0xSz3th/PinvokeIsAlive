
## For calling:
```cs
[ComVisible(false)]
[ComImport, InterfaceType(ComInterfaceType.InterfaceIsIUnknown), Guid("0000000A-0000-0000-C000-000000000046")]
public interface ILockBytes
{
    //Note: These two by(reference 32-bit integers (ULONG) could be used as return values instead,
    //      but they are not tagged [retval] in the IDL, so for consitency's sake...
    void ReadAt(long ulOffset, System.IntPtr pv, int cb, out System.UInt32 pcbRead);
    void WriteAt(long ulOffset, System.IntPtr pv, int cb, out System.UInt32 pcbWritten);
    void Flush();
    void SetSize(long cb);
    void LockRegion(long libOffset, long cb, int dwLockType);
    void UnlockRegion(long libOffset, long cb, int dwLockType);
    void Stat(out System.Runtime.InteropServices.STATSTG pstatstg, int grfStatFlag);

}
```

## For implementing:
```cs
[ComVisible(false)]
[ComImport, InterfaceType(ComInterfaceType.InterfaceIsIUnknown), Guid("0000000A-0000-0000-C000-000000000046")]
public interface ILockBytes
{
    //Note: Cannot rely on these two as by-reference parameters, because they are tagged __out_opt in the headers:
    //      This means some caller could pass a null pointer instead
    void ReadAt(long ulOffset, System.IntPtr pv, int cb, System.IntPtr pcbRead);
    void WriteAt(long ulOffset, System.IntPtr pv, int cb, System.IntPtr pcbWritten);
    void Flush();
    void SetSize(long cb);
    //Just ThrowExceptionForHR(STG_E_INVALIDFUNCTION) if locking is not supported.
    //Define it as a constant with the value unchecked((int)0x80030001u)
    void LockRegion(long libOffset, long cb, int dwLockType);
    void UnlockRegion(long libOffset, long cb, int dwLockType);
    void Stat(out System.Runtime.InteropServices.STATSTG pstatstg, int grfStatFlag);

}
```

## For implementing:
```cs
<InterfaceType(ComInterfaceType.InterfaceIsIUnknown), _
Guid("0000000a-0000-0000-C000-000000000046")> _
Public Interface IlockBytes
    Sub ReadAt(ByVal ulOffset As Long, ByVal pv As IntPtr, ByVal cv As Integer, <Out()> ByRef pcbRead As Integer)
    Sub WriteAt(ByVal ulOffset As Long, ByVal pv As IntPtr, ByVal cb As Integer, <Out()> ByRef pcbWritten As Integer)
    Sub Flush()
    Sub SetSize(ByVal cb As Long)
    Sub LockRegion(ByVal libOffset As Long, ByVal cb As Long, ByVal dwLockType As Integer)
    Sub UnlockRegion(ByVal libOffset As Long, ByVal cb As Long, ByVal dwLockType As Integer)
    Sub Stat(ByRef pstatstg As STATSTG, ByVal grfStatFlag As Integer)
End Interface
```

## Notes:
```cs
// read a chunk from the ILockBytes object
public int ReadAt(long offset, byte[] buffer, int bufferSize)
{
    IntPtr pv = Marshal.AllocHGlobal(bufferSize);
    UInt32 cbRead;

    ((ILockBytes)comPtr).ReadAt(offset, pv, bufferSize, out cbRead);

    int length = (int)cbRead;
    Marshal.Copy(pv, buffer, 0, length);

    Marshal.FreeHGlobal(pv);
    return length;
}
```
