
## C# Definition:
```cs
/// <summary>The IShellLink interface allows Shell links to be created, modified, and resolved</summary>
[ComImport(), InterfaceType(ComInterfaceType.InterfaceIsIUnknown), Guid("000214EE-0000-0000-C000-000000000046")]
interface IShellLinkA {
    /// <summary>Retrieves the path and file name of a Shell link object</summary>
    void GetPath([Out(), MarshalAs(UnmanagedType.LPStr)] StringBuilder pszFile, int cchMaxPath
        , out UnsafeNativeMethods.WIN32_FIND_DATAA pfd, UnsafeNativeMethods.SLGP_FLAGS fFlags);
    /// <summary>Retrieves the list of item identifiers for a Shell link object</summary>
    void GetIDList(out IntPtr ppidl);
    /// <summary>Sets the pointer to an item identifier list (PIDL) for a Shell link object</summary>
    void SetIDList(IntPtr pidl);
    /// <summary>Retrieves the description string for a Shell link object</summary>
    void GetDescription([Out(), MarshalAs(UnmanagedType.LPStr)] StringBuilder pszName, int cchMaxName);
    /// <summary>Sets the description for a Shell link object. The description can be any application-defined string</summary>
    void SetDescription([MarshalAs(UnmanagedType.LPStr)] string pszName);
    /// <summary>Retrieves the name of the working directory for a Shell link object</summary>
    void GetWorkingDirectory([Out(), MarshalAs(UnmanagedType.LPStr)] StringBuilder pszDir, int cchMaxPath);
    /// <summary>Sets the name of the working directory for a Shell link object</summary>
    void SetWorkingDirectory([MarshalAs(UnmanagedType.LPStr)] string pszDir);
    /// <summary>Retrieves the command-line arguments associated with a Shell link object</summary>
    void GetArguments([Out(), MarshalAs(UnmanagedType.LPStr)] StringBuilder pszArgs, int cchMaxPath);
    /// <summary>Sets the command-line arguments for a Shell link object</summary>
    void SetArguments([MarshalAs(UnmanagedType.LPStr)] string pszArgs);
    /// <summary>Retrieves the hot key for a Shell link object</summary>
    void GetHotkey(out short pwHotkey);
    /// <summary>Sets a hot key for a Shell link object</summary>
    void SetHotkey(short wHotkey);
    /// <summary>Retrieves the show command for a Shell link object</summary>
    void GetShowCmd(out int piShowCmd);
    /// <summary>Sets the show command for a Shell link object. The show command sets the initial show state of the window.</summary>
    void SetShowCmd(int iShowCmd);
    /// <summary>Retrieves the location (path and index) of the icon for a Shell link object</summary>
    void GetIconLocation([Out(), MarshalAs(UnmanagedType.LPStr)] StringBuilder pszIconPath
        , int cchIconPath, out int piIcon);
    /// <summary>Sets the location (path and index) of the icon for a Shell link object</summary>
    void SetIconLocation([MarshalAs(UnmanagedType.LPStr)] string pszIconPath, int iIcon);
    /// <summary>Sets the relative path to the Shell link object</summary>
    void SetRelativePath([MarshalAs(UnmanagedType.LPStr)] string pszPathRel, int dwReserved);
    /// <summary>Attempts to find the target of a Shell link, even if it has been moved or renamed</summary>
    void Resolve(IntPtr hwnd, UnsafeNativeMethods.SLR_FLAGS fFlags);
    /// <summary>Sets the path and file name of a Shell link object</summary>
    void SetPath([MarshalAs(UnmanagedType.LPStr)] string pszFile);
```

## VB Definition:
```cs
<ComImport> _
<Guid("TODO")> _
'TODO: Insert <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _ if this doesn't derive from IDispatch
Interface IShellLinkA
   TODO
End Interface
```

## VB.Net Definition:
```cs
<ComImportAttribute()> _
  <GuidAttribute("000214EE-0000-0000-C000-000000000046")> _
  <InterfaceTypeAttribute(ComInterfaceType.InterfaceIsIUnknown)> _
  Private Interface IShellLinkA
    '[helpstring("Retrieves the path and filename of a shell link object")]
    Sub GetPath(<Out(), MarshalAs(UnmanagedType.LPStr)> ByVal pszFile As StringBuilder, ByVal cchMaxPath As Integer, ByRef pfd As WIN32_FIND_DATAA, ByVal fFlags As UInteger)

    '[helpstring("Retrieves the list of shell link item identifiers")]
    Sub GetIDList(ByRef ppidl As IntPtr)

    '[helpstring("Sets the list of shell link item identifiers")]
    Sub SetIDList(ByVal pidl As IntPtr)

    '[helpstring("Retrieves the shell link description string")]
    Sub GetDescription(<Out(), MarshalAs(UnmanagedType.LPStr)> ByVal pszFile As StringBuilder, ByVal cchMaxName As Integer)

    '[helpstring("Sets the shell link description string")]
    Sub SetDescription(<MarshalAs(UnmanagedType.LPStr)> ByVal pszName As String)

    '[helpstring("Retrieves the name of the shell link working directory")]
    Sub GetWorkingDirectory(<Out(), MarshalAs(UnmanagedType.LPStr)> ByVal pszDir As StringBuilder, ByVal cchMaxPath As Integer)

    '[helpstring("Sets the name of the shell link working directory")]
    Sub SetWorkingDirectory(<MarshalAs(UnmanagedType.LPStr)> ByVal pszDir As String)

    '[helpstring("Retrieves the shell link command-line arguments")]
    Sub GetArguments(<Out(), MarshalAs(UnmanagedType.LPStr)> ByVal pszArgs As StringBuilder, ByVal cchMaxPath As Integer)

    '[helpstring("Sets the shell link command-line arguments")]
    Sub SetArguments(<MarshalAs(UnmanagedType.LPStr)> ByVal pszArgs As String)

    '[propget, helpstring("Retrieves or sets the shell link hot key")]
    Sub GetHotkey(ByRef pwHotkey As Short)
    '[propput, helpstring("Retrieves or sets the shell link hot key")]
    Sub SetHotkey(ByVal pwHotkey As Short)

    '[propget, helpstring("Retrieves or sets the shell link show command")]
    Sub GetShowCmd(ByRef piShowCmd As UInteger)
    '[propput, helpstring("Retrieves or sets the shell link show command")]
    Sub SetShowCmd(ByVal piShowCmd As UInteger)

    '[helpstring("Retrieves the location (path and index) of the shell link icon")]
    Sub GetIconLocation(<Out(), MarshalAs(UnmanagedType.LPStr)> ByVal pszIconPath As StringBuilder, ByVal cchIconPath As Integer, ByRef piIcon As Integer)

    '[helpstring("Sets the location (path and index) of the shell link icon")]
    Sub SetIconLocation(<MarshalAs(UnmanagedType.LPStr)> ByVal pszIconPath As String, ByVal iIcon As Integer)

    '[helpstring("Sets the shell link relative path")]
    Sub SetRelativePath(<MarshalAs(UnmanagedType.LPStr)> ByVal pszPathRel As String, ByVal dwReserved As UInteger)

    '[helpstring("Resolves a shell link. The system searches for the shell link object and updates the shell link path and its list of identifiers (if necessary)")]
    Sub Resolve(ByVal hWnd As IntPtr, ByVal fFlags As UInteger)

    '[helpstring("Sets the shell link path and filename")]
    Sub SetPath(<MarshalAs(UnmanagedType.LPStr)> ByVal pszFile As String)
  End Interface
```
