
## C# Definition:
```cs
/// <summary>The IShellLink interface allows Shell links to be created, modified, and resolved</summary>
[ComImport(), InterfaceType(ComInterfaceType.InterfaceIsIUnknown), Guid("000214F9-0000-0000-C000-000000000046")]
interface IShellLinkW 
{
    /// <summary>Retrieves the path and file name of a Shell link object</summary>
    void GetPath([Out(), MarshalAs(UnmanagedType.LPWStr)] StringBuilder pszFile, int cchMaxPath, out UnsafeNativeMethods.WIN32_FIND_DATAW pfd, UnsafeNativeMethods.SLGP_FLAGS fFlags);
    /// <summary>Retrieves the list of item identifiers for a Shell link object</summary>
    void GetIDList(out IntPtr ppidl);
    /// <summary>Sets the pointer to an item identifier list (PIDL) for a Shell link object.</summary>
    void SetIDList(IntPtr pidl);
    /// <summary>Retrieves the description string for a Shell link object</summary>
    void GetDescription([Out(), MarshalAs(UnmanagedType.LPWStr)] StringBuilder pszName, int cchMaxName);
    /// <summary>Sets the description for a Shell link object. The description can be any application-defined string</summary>
    void SetDescription([MarshalAs(UnmanagedType.LPWStr)] string pszName);
    /// <summary>Retrieves the name of the working directory for a Shell link object</summary>
    void GetWorkingDirectory([Out(), MarshalAs(UnmanagedType.LPWStr)] StringBuilder pszDir, int cchMaxPath);
    /// <summary>Sets the name of the working directory for a Shell link object</summary>
    void SetWorkingDirectory([MarshalAs(UnmanagedType.LPWStr)] string pszDir);
    /// <summary>Retrieves the command-line arguments associated with a Shell link object</summary>
    void GetArguments([Out(), MarshalAs(UnmanagedType.LPWStr)] StringBuilder pszArgs, int cchMaxPath);
    /// <summary>Sets the command-line arguments for a Shell link object</summary>
    void SetArguments([MarshalAs(UnmanagedType.LPWStr)] string pszArgs);
    /// <summary>Retrieves the hot key for a Shell link object</summary>
    void GetHotkey(out short pwHotkey);
    /// <summary>Sets a hot key for a Shell link object</summary>
    void SetHotkey(short wHotkey);
    /// <summary>Retrieves the show command for a Shell link object</summary>
    void GetShowCmd(out int piShowCmd);
    /// <summary>Sets the show command for a Shell link object. The show command sets the initial show state of the window.</summary>
    void SetShowCmd(int iShowCmd);
    /// <summary>Retrieves the location (path and index) of the icon for a Shell link object</summary>
    void GetIconLocation([Out(), MarshalAs(UnmanagedType.LPWStr)] StringBuilder pszIconPath,
        int cchIconPath, out int piIcon);
    /// <summary>Sets the location (path and index) of the icon for a Shell link object</summary>
    void SetIconLocation([MarshalAs(UnmanagedType.LPWStr)] string pszIconPath, int iIcon);
    /// <summary>Sets the relative path to the Shell link object</summary>
    void SetRelativePath([MarshalAs(UnmanagedType.LPWStr)] string pszPathRel, int dwReserved);
    /// <summary>Attempts to find the target of a Shell link, even if it has been moved or renamed</summary>
    void Resolve(IntPtr hwnd, UnsafeNativeMethods.SLR_FLAGS fFlags);
    /// <summary>Sets the path and file name of a Shell link object</summary>
    void SetPath([MarshalAs(UnmanagedType.LPWStr)] string pszFile);
}
```

## VB Definition:
```cs
<ComVisible(True), ComImport(), Guid("000214F9-0000-0000-C000-000000000046"), _
    InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _
    Public Interface IShellLinkW
    ''' <summary>Retrieves the path and file name of a Shell link object</summary>
    <PreserveSig()> Function GetPath( _
            <MarshalAs(UnmanagedType.LPWStr)> ByVal pszFile As Text.StringBuilder, _
            ByVal cch As Integer, _
            ByRef pfd As WIN32_FIND_DATA, _
            ByVal fFlags As Integer) As HRESULT
    ''' <summary>Retrieves the list of item identifiers for a Shell link object</summary>
    <PreserveSig()> Function GetIDList(ByRef ppidl As IntPtr) As HRESULT
    ''' <summary>Sets the pointer to an item identifier list (PIDL) for a Shell link object.</summary>
    <PreserveSig()> Function SetIDList(ByVal pidl As IntPtr) As HRESULT
    ''' <summary>Retrieves the description string for a Shell link object</summary>
    <PreserveSig()> Function GetDescription( _
            <MarshalAs(UnmanagedType.LPWStr)> ByVal pszName As Text.StringBuilder, _
            ByVal cch As Integer) As HRESULT
    ''' <summary>Sets the description for a Shell link object. The description can be any application-defined string</summary>
    <PreserveSig()> Function SetDescription( _
            <MarshalAs(UnmanagedType.LPWStr)> ByVal pszName As String) As HRESULT
    ''' <summary>Retrieves the name of the working directory for a Shell link object</summary>
    <PreserveSig()> Function GetWorkingDirectory( _
            <MarshalAs(UnmanagedType.LPWStr)> ByVal pszDir As Text.StringBuilder, _
            ByVal cch As Integer) As HRESULT
    ''' <summary>Sets the name of the working directory for a Shell link object</summary>
    <PreserveSig()> Function SetWorkingDirectory( _
            <MarshalAs(UnmanagedType.LPWStr)> ByVal pszDir As String) As HRESULT
    ''' <summary>Retrieves the command-line arguments associated with a Shell link object</summary>
    <PreserveSig()> Function GetArguments( _
            <MarshalAs(UnmanagedType.LPWStr)> ByVal pszArgs As Text.StringBuilder, _
            ByVal cch As Integer) As HRESULT
    ''' <summary>Sets the command-line arguments for a Shell link object</summary>
    <PreserveSig()> Function SetArguments( _
            <MarshalAs(UnmanagedType.LPWStr)> ByVal pszArgs As String) As HRESULT
    ''' <summary>Retrieves the hot key for a Shell link object</summary>
    <PreserveSig()> Function GetHotkey(ByRef pwHotkey As Short) As HRESULT
    ''' <summary>Sets a hot key for a Shell link object</summary>
    <PreserveSig()> Function SetHotkey(ByVal wHotkey As Short) As HRESULT
    ''' <summary>Retrieves the show command for a Shell link object</summary>
    <PreserveSig()> Function GetShowCmd(ByRef piShowCmd As Integer) As HRESULT
    ''' <summary>Sets the show command for a Shell link object. The show command sets the initial show state of the window.</summary>
    <PreserveSig()> Function SetShowCmd(ByVal iShowCmd As Integer) As HRESULT
    ''' <summary>Retrieves the location (path and index) of the icon for a Shell link object</summary>
    <PreserveSig()> Function GetIconLocation( _
            <MarshalAs(UnmanagedType.LPWStr)> ByVal pszIconPath As Text.StringBuilder, _
            ByVal cch As Integer, _
            ByRef piIcon As Integer) As HRESULT
    ''' <summary>Sets the location (path and index) of the icon for a Shell link object</summary>
    <PreserveSig()> Function SetIconLocation( _
            <MarshalAs(UnmanagedType.LPWStr)> ByVal pszIconPath As String, _
            ByVal iIcon As Integer) As HRESULT
    ''' <summary>Sets the relative path to the Shell link object</summary>
    <PreserveSig()> Function SetRelativePath( _
            <MarshalAs(UnmanagedType.LPWStr)> ByVal pszPathRel As String, _
            ByVal dwReserved As Integer) As HRESULT
    ''' <summary>Attempts to find the target of a Shell link, even if it has been moved or renamed</summary>
    <PreserveSig()> Function Resolve(ByVal hwnd As IntPtr, ByVal fFlags As Integer) As HRESULT
    ''' <summary>Sets the path and file name of a Shell link object</summary>
    <PreserveSig()> Function SetPath( _
            <MarshalAs(UnmanagedType.LPWStr)> ByVal pszFile As String) As HRESULT

End Interface
```

## Notes:
```cs
Type    obj = Type.GetTypeFromCLSID(new Guid("00021401-0000-0000-C000-000000000046"), true);
IShellLinkW lnk = Activator.CreateInstance(obj) as IShellLinkW;
```

## Notes:
```cs
lnk.SetPath("c:\\thefile.txt");
((IPersistFile)lnk).Save("c:\\thelink.LNK", true);
```
