
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
        public struct WLAN_INTERFACE_INFO
        {
        /// GUID->_GUID
        public Guid InterfaceGuid;

        /// WCHAR[256]
        [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 256)]
        public string strInterfaceDescription;

        /// WLAN_INTERFACE_STATE->_WLAN_INTERFACE_STATE
        public WLAN_INTERFACE_STATE isState;
        }
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential, CharSet := CharSet.Unicode)> _
     Public Structure WLAN_INTERFACE_INFO
     ''' GUID->_GUID
     Public InterfaceGuid As Guid

     ''' WCHAR[256]
     <MarshalAs(UnmanagedType.ByValTStr, SizeConst := 256)> _
     Public strInterfaceDescription As String

     ''' WLAN_INTERFACE_STATE->_WLAN_INTERFACE_STATE
     Public isState As WLAN_INTERFACE_STATE
     End Structure
```
