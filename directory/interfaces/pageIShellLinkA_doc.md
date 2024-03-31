
## C# Definition:
```cs
[ComImport]
[Guid("00021401-0000-0000-C000-000000000046")]
internal class ShellLink
{
}

[ComImport]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
[Guid("000214F9-0000-0000-C000-000000000046")]
internal interface IShellLink
{
    void GetPath([Out, MarshalAs(UnmanagedType.LPWStr)] StringBuilder pszFile, int cchMaxPath, out IntPtr pfd, int fFlags);
    void GetIDList(out IntPtr ppidl); 
    void SetIDList(IntPtr pidl);
    void GetDescription([Out, MarshalAs(UnmanagedType.LPWStr)] StringBuilder pszName, int cchMaxName);
    void SetDescription([MarshalAs(UnmanagedType.LPWStr)] string pszName);
    void GetWorkingDirectory([Out, MarshalAs(UnmanagedType.LPWStr)] StringBuilder pszDir, int cchMaxPath);
    void SetWorkingDirectory([MarshalAs(UnmanagedType.LPWStr)] string pszDir);
    void GetArguments([Out, MarshalAs(UnmanagedType.LPWStr)] StringBuilder pszArgs, int cchMaxPath);
    void SetArguments([MarshalAs(UnmanagedType.LPWStr)] string pszArgs);
    void GetHotkey(out short pwHotkey);
    void SetHotkey(short wHotkey);
    void GetShowCmd(out int piShowCmd);
    void SetShowCmd(int iShowCmd);
    void GetIconLocation([Out, MarshalAs(UnmanagedType.LPWStr)] StringBuilder pszIconPath, int cchIconPath, out int piIcon);
    void SetIconLocation([MarshalAs(UnmanagedType.LPWStr)] string pszIconPath, int iIcon);
    void SetRelativePath([MarshalAs(UnmanagedType.LPWStr)] string pszPathRel, int dwReserved);
    void Resolve(IntPtr hwnd, int fFlags);
    void SetPath([MarshalAs(UnmanagedType.LPWStr)] string pszFile);
}
```

## VB Definition:
```cs
<ComImport(), Guid("00021401-0000-0000-C000-000000000046")>
Private Class ShellLink
End Class

<ComImport(), InterfaceType(ComInterfaceType.InterfaceIsIUnknown), Guid("000214F9-0000-0000-C000-000000000046")>
Private Interface IShellLink
    Sub GetPath(<Out, MarshalAs(UnmanagedType.LPWStr)> ByVal pszFile As StringBuilder, ByVal cchMaxPath As Integer, <Out> ByRef pfd As IntPtr, ByVal fFlags As Integer)
    Sub GetIDList(<Out> ByRef ppidl As IntPtr)
    Sub SetIDList(ByVal pidl As IntPtr)
    Sub GetDescription(<Out, MarshalAs(UnmanagedType.LPWStr)> ByVal pszName As StringBuilder, ByVal cchMaxName As Integer)
    Sub SetDescription(<MarshalAs(UnmanagedType.LPWStr)> ByVal pszName As String)
    Sub GetWorkingDirectory(<Out, MarshalAs(UnmanagedType.LPWStr)> ByVal pszDir As StringBuilder, ByVal cchMaxPath As Integer)
    Sub SetWorkingDirectory(<MarshalAs(UnmanagedType.LPWStr)> ByVal pszDir As String)
    Sub GetArguments(<Out, MarshalAs(UnmanagedType.LPWStr)> ByVal pszArgs As StringBuilder, ByVal cchMaxPath As Integer)
    Sub SetArguments(<MarshalAs(UnmanagedType.LPWStr)> ByVal pszArgs As String)
    Sub GetHotkey(<Out> ByRef pwHotkey As Short)
    Sub SetHotkey(ByVal wHotkey As Short)
    Sub GetShowCmd(<Out> ByRef piShowCmd As Integer)
    Sub SetShowCmd(ByVal iShowCmd As Integer)
    Sub GetIconLocation(<Out, MarshalAs(UnmanagedType.LPWStr)> ByVal pszIconPath As StringBuilder, ByVal cchIconPath As Integer, <Out> ByRef piIcon As Integer)
    Sub SetIconLocation(<MarshalAs(UnmanagedType.LPWStr)> ByVal pszIconPath As String, ByVal iIcon As Integer)
    Sub SetRelativePath(<MarshalAs(UnmanagedType.LPWStr)> ByVal pszPathRel As String, ByVal dwReserved As Integer)
    Sub Resolve(ByVal hwnd As IntPtr, ByVal fFlags As Integer)
    Sub SetPath(<MarshalAs(UnmanagedType.LPWStr)> ByVal pszFile As String)
End Interface
```

## How to use example (VB):
```cs
Public Shared Sub CreateNewShortcut(LNKLocation As String, LNKTarget As String, Optional TargetArgs As String = Nothing, Optional StartFolder As String = Nothing,
                                       Optional Description As String = Nothing, Optional IconFile As String = "c:\windows\System32\SHELL32.dll", Optional IconIndex As Integer = 21)

    Dim link As IShellLink = CType(New ShellLink(), IShellLink)

    If Description <> Nothing Then link.SetDescription(Description)
    If TargetArgs <> Nothing Then link.SetArguments(TargetArgs)
    If IconFile <> Nothing Then link.SetIconLocation(IconFile, IconIndex)

    link.SetPath(LNKTarget)

    Dim file As System.Runtime.InteropServices.ComTypes.IPersistFile = CType(link, ComTypes.IPersistFile)
    file.Save(LNKLocation, False)

    link.SetPath("C:\windows\System32\calc.exe")
End Sub
```
