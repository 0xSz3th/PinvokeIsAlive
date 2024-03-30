
## C# Definition:
```cs
[StructLayout (LayoutKind.Sequential)]
    public struct CMINVOKECOMMANDINFOEX {
        public int            cbSize;        // Marshal.SizeOf(CMINVOKECOMMANDINFO)
        public int            fMask;         // any combination of CMIC_MASK_*
        public IntPtr        hwnd;          // might be NULL (indicating no owner window)
        public string        lpVerb;        // either a string or MAKEINTRESOURCE(idOffset)
        public string        lpParameters;      // might be NULL (indicating no parameter)
        public string        lpDirectory;       // might be NULL (indicating no specific directory)
        public int            nShow;         // one of SW_ values for ShowWindow() API
        public int            dwHotKey;        // Optional hot key to assign to any application activated by the command. If the fMask member does not specify CMIC_MASK_HOTKEY, this member is ignored. 
        public IntPtr        hIcon;            // Icon to use for any application activated by the command. If the fMask member does not specify CMIC_MASK_ICON, this member is ignored. 

        public string        lpTitle;        // ASCII title.

        [MarshalAs(UnmanagedType.LPWStr)]
        public string        lpVerbW;                // Unicode verb, for those commands that can use it.

        [MarshalAs(UnmanagedType.LPWStr)]
        public string        lpParametersW;        // Unicode parameters, for those commands that can use it. 

        [MarshalAs(UnmanagedType.LPWStr)]
        public string        lpDirectoryW;        // Unicode directory, for those commands that can use it.

        [MarshalAs(UnmanagedType.LPWStr)]
        public string        lpTitleW;            // Unicode title.

        public POINT        ptInvoke;                // Point where the command is invoked. This member is not valid prior to Microsoft Internet Explorer 4.0.
    }
```

## VB Definition:
```cs
Structure CMINVOKECOMMANDINFOEX 
   Public TODO
End Structure
```
