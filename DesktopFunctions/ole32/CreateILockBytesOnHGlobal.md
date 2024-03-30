
## C# Signature:
```cs
/// <summary>
    /// The CreateILockBytesOnHGlobal function creates a byte array object, 
    /// using global memory as the physical device, which is intended to be the 
    /// compound file foundation. This object supports a COM implementation of the 
    /// ILockBytes interface.
    /// </summary>
    /// 
    /// <param name="hGlobal">The memory handle allocated by the GlobalAlloc function. 
    /// The handle must be allocated as moveable and nondiscardable. If the handle is 
    /// shared between processes, it must also be allocated as shared. New handles should 
    /// be allocated with a size of zero. If hGlobal is NULL, CreateILockBytesOnHGlobal 
    /// internally allocates a new shared memory block of size zero.</param>
    /// 
    /// <param name="fDeleteOnRelease">A flag that specifies whether the underlying handle 
    /// for this byte array object should be automatically freed when the object is released. 
    /// If set to FALSE, the caller must free the hGlobal after the final release. If set 
    /// to TRUE, the final release will automatically free the hGlobal parameter.</param>
    /// 
    /// <param name="ppLkbyt">The address of ILockBytes pointer variable that receives the 
    /// interface pointer to the new byte array object.</param>
    /// 
    /// <returns>This function supports the standard return values E_INVALIDARG and E_OUTOFMEMORY, as well as the following:
    /// S_OK: The byte array object was created successfully.</returns>
    [DllImport ("ole32.dll")]
    public extern static int CreateILockBytesOnHGlobal(IntPtr hGlobal, [MarshalAs(UnmanagedType.Bool)] bool fDeleteOnRelease, out ILockBytes ppLkbyt);
```

## C# Signature:
```cs
[DllImport("ole32.dll",
    EntryPoint="CreateILockBytesOnHGlobal",
    ExactSpelling=true, PreserveSig=true, CharSet=CharSet.Ansi,
    CallingConvention=CallingConvention.StdCall)]
static extern int CreateILockBytesOnHGlobal(IntPtr /* HGLOBAL */ hGlobal, bool fDeleteOnRelease, [MarshalAs(UnmanagedType.Interface)]out object /* ILockBytes** */ ppLkbyt);
```

## VB.NET Signature:
```cs
<DllImport("ole32.dll")> _
    Public Shared Function CreateILockBytesOnHGlobal(ByVal hGlobal As IntPtr, _
                              ByVal fDeleteOnRelease As Boolean, _
                              <Out()> ByRef ppLkbyt As IlockBytes) _
                              As Integer
    End Function
```
