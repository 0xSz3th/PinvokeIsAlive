
## VB Signature:
```cs
<StructLayout(LayoutKind.Explicit, Size:=80)> _
    Public Structure INTERNET_CACHE_ENTRY_INFOA
    <FieldOffset(0)> Public dwStructSize As UInt32
    <FieldOffset(4)> Public lpszSourceUrlName As IntPtr
    <FieldOffset(8)> Public lpszLocalFileName As IntPtr
    <FieldOffset(12)> Public CacheEntryType As UInt32
    <FieldOffset(16)> Public dwUseCount As UInt32
    <FieldOffset(20)> Public dwHitRate As UInt32
    <FieldOffset(24)> Public dwSizeLow As UInt32
    <FieldOffset(28)> Public dwSizeHigh As UInt32
    <FieldOffset(32)> Public LastModifiedTime As FILETIME
    <FieldOffset(40)> Public ExpireTime As FILETIME
    <FieldOffset(48)> Public LastAccessTime As FILETIME
    <FieldOffset(56)> Public LastSyncTime As FILETIME
    <FieldOffset(64)> Public lpHeaderInfo As IntPtr
    <FieldOffset(68)> Public dwHeaderInfoSize As UInt32
    <FieldOffset(72)> Public lpszFileExtension As IntPtr
    <FieldOffset(76)> Public dwReserved As UInt32
    <FieldOffset(76)> Public dwExemptDelta As UInt32
    End Structure
```
