# SHARE\_INFO\_502

IntPtr bufptr = IntPtr.Zero;         int err;         IntPtr ptr = IntPtr.Zero;         int output = NetShareGetInfo("", @"", 502, out ptr);         SHARE\_INFO\_502 shareInfo = (SHARE\_INFO\_502)Marshal.PtrToStructure(ptr, typeof(SHARE\_INFO\_502));

### C# Definition:

```cs
[StructLayout(LayoutKind.Sequential)]
    public struct SHARE_INFO_502
    {
        [MarshalAs(UnmanagedType.LPWStr)]
        public string shi502_netname;
        public uint shi502_type;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string shi502_remark;
        public Int32 shi502_permissions;
        public Int32 shi502_max_uses;
        public Int32 shi502_current_uses;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string shi502_path;
        public IntPtr shi502_passwd;
        public Int32 shi502_reserved;
        public IntPtr shi502_security_descriptor;
    }
```

### VB Definition:

```cs
Structure SHARE_INFO_502 
   Public TODO
End Structure
```
