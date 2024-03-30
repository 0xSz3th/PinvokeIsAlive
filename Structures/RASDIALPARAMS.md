
## C# Definitions:
```cs
[StructLayout(LayoutKind.Sequential,CharSet = CharSet.Auto)]
struct RASDIALPARAMS {
   public int  dwSize; 
   [MarshalAs(UnmanagedType.ByValTStr, SizeConst = Constants.RAS_MaxEntryName + 1)]
   public string szEntryName; 
   [MarshalAs(UnmanagedType.ByValTStr, SizeConst = Constants.RAS_MaxPhoneNumber + 1)]
   public string szPhoneNumber; 
   [MarshalAs(UnmanagedType.ByValTStr, SizeConst = Constants.RAS_MaxCallbackNumber + 1)]
   public string szCallbackNumber; 
   [MarshalAs(UnmanagedType.ByValTStr, SizeConst = Constants.UsernameLength + 1)]
   public string szUserName;
   [MarshalAs(UnmanagedType.ByValTStr, SizeConst = Constants.PasswordLength + 1)]
   public string szPassword; 
   [MarshalAs(UnmanagedType.ByValTStr, SizeConst = Constants.DomainLength + 1)]
   public string szDomain;
   public uint    dwSubEntry;
   public IntPtr dwCallbackId;
}
```

## VB Definition:
```cs
Structure RASDIALPARAMS 
   Public TODO
End Structure
```
