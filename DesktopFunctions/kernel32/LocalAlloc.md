
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern IntPtr LocalAlloc(uint uFlags, UIntPtr uBytes);
```

## User-Defined Types:
```cs
[Flags]
public enum LocalMemoryFlags {
    LMEM_FIXED = 0x0000,
    LMEM_MOVEABLE = 0x0002,
    LMEM_NOCOMPACT = 0x0010,
    LMEM_NODISCARD = 0x0020,
    LMEM_ZEROINIT = 0x0040,
    LMEM_MODIFY = 0x0080,
    LMEM_DISCARDABLE = 0x0F00,
    LMEM_VALID_FLAGS = 0x0F72,
    LMEM_INVALID_HANDLE = 0x8000,
    LHND = (LMEM_MOVEABLE | LMEM_ZEROINIT),
    LPTR = (LMEM_FIXED | LMEM_ZEROINIT),
    NONZEROLHND = (LMEM_MOVEABLE),
    NONZEROLPTR = (LMEM_FIXED)
}
```

## Sample Code:
```cs
public IntPtr Alloc(int size) {
    // Allocate the memory, zeroing it in the progress
    IntPtr memPtr = LocalAlloc(LocalMemoryFlags.LPTR, new UIntPtr((uint)size));
    // Throw an OutOfMemoryException if out of memory
    if (memPtr == IntPtr.Zero)
        throw new OutOfMemoryException();
    return memPtr;
}
```
