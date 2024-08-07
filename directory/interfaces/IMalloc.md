
## C# Definition:
```cs
/// <summary>
/// C# definition of the IMalloc interface.
/// </summary>
[ComImport]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
[Guid("00000002-0000-0000-C000-000000000046")]
internal interface IMalloc
{
    /// <summary>
    /// Allocate a block of memory
    /// </summary>
    /// <param name="cb">Size, in bytes, of the memory block to be allocated.</param>
    /// <returns>a pointer to the allocated memory block.</returns>
    [PreserveSig]
    IntPtr Alloc(
        [In] UInt32 cb);

    /// <summary>
    /// Changes the size of a previously allocated memory block.
    /// </summary>
    /// <param name="pv">Pointer to the memory block to be reallocated</param>
    /// <param name="cb">Size of the memory block, in bytes, to be reallocated.</param>
    /// <returns>reallocated memory block</returns>
    [PreserveSig]
    IntPtr Realloc(
        [In] IntPtr pv,
        [In] UInt32 cb);

    /// <summary>
    /// Free a previously allocated block of memory.
    /// </summary>
    /// <param name="pv">Pointer to the memory block to be freed.</param>
    [PreserveSig]
    void Free(
        [In] IntPtr pv);

    /// <summary>
    /// This method returns the size, in bytes, of a memory block previously allocated with IMalloc::Alloc or IMalloc::Realloc.
    /// </summary>
    /// <param name="pv">Pointer to the memory block for which the size is requested</param>
    /// <returns>The size of the allocated memory block in bytes.</returns>
    [PreserveSig]
    UInt32 GetSize(
        [In] IntPtr pv);

    /// <summary>
    /// This method determines whether this allocator was used to allocate the specified block of memory.
    /// </summary>
    /// <param name="pv">Pointer to the memory block</param>
    /// <returns>
    /// 1 - allocated 
    /// 0 - not allocated by this IMalloc Instance.
    /// -1 if DidAlloc is unable to determine whether or not it allocated the memory block.
    /// </returns>
    [PreserveSig]
    Int16 DidAlloc(
        [In] IntPtr pv);

    /// <summary>
    /// Minimizes the heap by releasing unused memory to the operating system.
    /// </summary>
    [PreserveSig]
    void HeapMinimize();
}
```

## VB Definition:
```cs
<Runtime.InteropServices.ComImport()> _
<Runtime.InteropServices.InterfaceType(Runtime.InteropServices.ComInterfaceType.InterfaceIsIUnknown)> _
<Runtime.InteropServices.Guid("00000002-0000-0000-C000-000000000046")> _
Public Interface IMalloc

    ''' <summary>
    ''' Allocate a block of Memory.
    ''' </summary>
    ''' <param name="cb">Size, in bytes, of the memory block to be allocated.</param>
    ''' <returns>Returns a pointer to the allocated memory block.</returns>
    <Runtime.InteropServices.PreserveSig()> Function Alloc(ByVal cb As UInt32) As IntPtr

    ''' <summary>
    ''' Changes the size of the allocated memory block.
    ''' </summary>
    ''' <param name="pv">Pointer to the memory block to be reallocated.</param>
    ''' <param name="cb">Size of the memory block, in bytes, to be reallocated.</param>
    ''' <returns>Returns the reallocated memory block.</returns>
    <Runtime.InteropServices.PreserveSig()> Function Realloc(ByVal pv As IntPtr, ByVal cb As UInt32) As IntPtr

    ''' <summary>
    ''' Free a previously allocated block of memory.
    ''' </summary>
    ''' <param name="pv">Pointer to the memory block to be freed.</param>
    <Runtime.InteropServices.PreserveSig()> Sub Free(ByVal pv As IntPtr)

    ''' <summary>
    ''' This method returns the size, in bytes, of a memory block previously allocated with IMalloc::Alloc or IMalloc::Realloc.
    ''' </summary>
    ''' <param name="pv">Pointer to the memory block for which the size is requested.</param>
    ''' <returns>Returns the size of the allocated memory block in bytes.</returns>
    <Runtime.InteropServices.PreserveSig()> Function GetSize(ByVal pv As IntPtr) As UInt32

    ''' <summary>
    ''' This method determines whether this allocator was used to allocate the specified block of memory.
    ''' </summary>
    ''' <param name="pv">Pointer to the memory block.</param>
    ''' <returns>1 - allocated 0 - not allocated by this IMalloc Instance.</returns>
    <Runtime.InteropServices.PreserveSig()> Function DidAlloc(ByVal pv As IntPtr) As Int16

    ''' <summary>
    ''' 'Minimizes the heap by releasing unused memory to the operating system.
    ''' </summary>
    <Runtime.InteropServices.PreserveSig()> Sub HeapMinimize()

End Interface
The IMalloc interface allocates, frees, and manages memory.11/7/2011 6:34:00 PM - -24.178.72.89
```
