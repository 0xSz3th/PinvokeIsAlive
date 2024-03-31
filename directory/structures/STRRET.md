
## C# Definition:
```cs
[StructLayout(LayoutKind.Explicit, Size=264)]
public struct STRRET
{
     [FieldOffset(0)]
     public UInt32 uType;    // One of the STRRET_* values

     [FieldOffset(4)]
     public IntPtr pOleStr;    // must be freed by caller of GetDisplayNameOf

     [FieldOffset(4)]
     public IntPtr pStr;        // NOT USED

     [FieldOffset(4)]
     public UInt32 uOffset;    // Offset into SHITEMID

     [FieldOffset(4)]
     public IntPtr cStr;        // Buffer to fill in (ANSI)
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Explicit, Size=264)> _
     Public Structure STRRET
     <FieldOffset(0)> Public uType As UInt32     'One of the STRRET_* values
     <FieldOffset(4)> Public pOleStr As IntPtr   'must be freed by caller of GetDisplayNameOf
     <FieldOffset(4)> Public pStr As IntPtr      'NOT USED
     <FieldOffset(4)> Public uOffset As UInt32   'Offset into SHITEMID
     <FieldOffset(4)> Public cString As IntPtr   'Buffer to fill in (ANSI)
     End Structure
```

## Notes:
```cs
Example:
// Structure used to return the display name to
STRRET pDisplayName;
String DisplayName;
SHFILEINFO m_shfi = new SHFILEINFO();

// Request the string as a char although Windows will likely ignore
// the request.
pDisplayName.uType = (uint)STRRET_TYPE.STRRET_CSTR;

// Get the "normal" display name.
iShellFolder.GetDisplayNameOf(pidlItems[0], SHGNO.SHGDN_NORMAL, 
         out pDisplayName);
System.Text.StringBuilder sbDisplayName = new System.Text.StringBuilder(256);
// Get the display name from the STRRET structure
WindowsAPI.StrRetToBuf(ref pDisplayName, pidlItems[0], 
        sbDisplayName, (uint)sbDisplayName.Capacity);
DisplayName = sbDisplayName.ToString();
```
