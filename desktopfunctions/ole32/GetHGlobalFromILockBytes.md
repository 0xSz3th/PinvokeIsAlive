
## C# Signature:
```cs
/// <summary>
    /// The GetHGlobalFromILockBytes function retrieves a global memory handle to a 
    /// byte array object created using the CreateILockBytesOnHGlobal function.
    /// </summary>
    /// 
    /// <param name="pLkbyt">Pointer to the ILockBytes interface on the byte-array 
    /// object previously created by a call to the CreateILockBytesOnHGlobal function.</param>
    /// 
    /// <param name="phglobal">Pointer to the current memory handle used by the 
    /// specified byte-array object.</param>
    /// 
    /// <returns></returns>
    [DllImport("ole32.dll")]
    static extern int GetHGlobalFromILockBytes(ILockBytes pLkbyt, out IntPtr phglobal);
```

## C# Signature:
```cs
[DllImport("ole32.dll",
     EntryPoint="GetHGlobalFromILockBytes",
     ExactSpelling=true, PreserveSig=true, CharSet=CharSet.Ansi,
     CallingConvention=CallingConvention.StdCall)]
static extern int GetHGlobalFromILockBytes([MarshalAs(UnmanagedType.Interface)] object /* ILockBytes* */pLkbyt, out IntPtr /* HGLOBAL* */ phglobal);
```
