
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct CIDA
    {
    /// <summary>
    ///  Number of PIDLs that are being transferred, not counting the parent folder.
    /// </summary>
    public uint cidl;

    /// <summary>
    /// An array of offsets, relative to the beginning of this structure. The array contains
    /// cidl+1 elements. The first element of aoffset contains an offset to the fully-qualified
    /// PIDL of a parent foloder. If this PIDL is empty, the parent folder is the desktop.
    /// Each of the remaining elements of the array contains an offset to one of the PIDLs to be 
    /// transferred. ALL of these PIDLs are relative to the PIDL of the parent folder.
    /// </summary>
    [MarshalAs(UnmanagedType.ByValArray, SizeConst = 1)]
    public uint[] aoffset;
    }
```

## VB Definition:
```cs
Structure CIDA 
   Public TODO
End Structure
```
