
## C# Definition:
```cs
[Flags]
public enum BrowseInfoFlags : uint
{
    /// <summary>
    /// Only return file system directories. 
    /// 
    /// If the user selects folders that are not part of the file system, 
    /// the OK button is grayed. 
    /// </summary>
    BIF_RETURNONLYFSDIRS = 0x00000001,
    /// <summary>
    /// Do not include network folders below the domain level in the dialog box's tree view control.
    /// </summary>
    BIF_DONTGOBELOWDOMAIN = 0x00000002,
    /// <summary>
    /// Include a status area in the dialog box. 
    /// The callback function can set the status text by sending messages to the dialog box. 
    /// This flag is not supported when <bold>BIF_NEWDIALOGSTYLE</bold> is specified
    /// </summary>
    BIF_STATUSTEXT = 0x00000004,
    /// <summary>
    /// Only return file system ancestors. 
    /// An ancestor is a subfolder that is beneath the root folder in the namespace hierarchy. 
    /// If the user selects an ancestor of the root folder that is not part of the file system, the OK button is grayed
    /// </summary>
    BIF_RETURNFSANCESTORS = 0x00000008,
    /// <summary>
    /// Include an edit control in the browse dialog box that allows the user to type the name of an item.
    /// </summary>
    BIF_EDITBOX = 0x00000010,
    /// <summary>
    /// If the user types an invalid name into the edit box, the browse dialog box calls the application's BrowseCallbackProc with the BFFM_VALIDATEFAILED message. 
    /// This flag is ignored if <bold>BIF_EDITBOX</bold> is not specified.
    /// </summary>
    BIF_VALIDATE = 0x00000020,
    /// <summary>
    /// Use the new user interface. 
    /// Setting this flag provides the user with a larger dialog box that can be resized. 
    /// The dialog box has several new capabilities, including: drag-and-drop capability within the 
    /// dialog box, reordering, shortcut menus, new folders, delete, and other shortcut menu commands. 
    /// </summary>
    BIF_NEWDIALOGSTYLE = 0x00000040,
    /// <summary>
    /// The browse dialog box can display URLs. The <bold>BIF_USENEWUI</bold> and <bold>BIF_BROWSEINCLUDEFILES</bold> flags must also be set. 
    /// If any of these three flags are not set, the browser dialog box rejects URLs.
    /// </summary>
    BIF_BROWSEINCLUDEURLS = 0x00000080,
    /// <summary>
    /// Use the new user interface, including an edit box. This flag is equivalent to <bold>BIF_EDITBOX | BIF_NEWDIALOGSTYLE</bold>
    /// </summary>
    BIF_USENEWUI = (BIF_EDITBOX | BIF_NEWDIALOGSTYLE),
    /// <summary>
    /// hen combined with <bold>BIF_NEWDIALOGSTYLE</bold>, adds a usage hint to the dialog box, in place of the edit box. <bold>BIF_EDITBOX</bold> overrides this flag.
    /// </summary>
    BIF_UAHINT = 0x00000100,
    /// <summary>
    /// Do not include the New Folder button in the browse dialog box.
    /// </summary>
    BIF_NONEWFOLDERBUTTON = 0x00000200,
    /// <summary>
    /// When the selected item is a shortcut, return the PIDL of the shortcut itself rather than its target.
    /// </summary>
    BIF_NOTRANSLATETARGETS = 0x00000400,
    /// <summary>
    /// Only return computers. If the user selects anything other than a computer, the OK button is grayed.
    /// </summary>
    BIF_BROWSEFORCOMPUTER = 0x00001000,
    /// <summary>
    /// Only allow the selection of printers. If the user selects anything other than a printer, the OK button is grayed
    /// </summary>
    BIF_BROWSEFORPRINTER = 0x00002000,
    /// <summary>
    /// The browse dialog box displays files as well as folders.
    /// </summary>
    BIF_BROWSEINCLUDEFILES = 0x00004000,
    /// <summary>
    /// The browse dialog box can display shareable resources on remote systems.
    /// </summary>
    BIF_SHAREABLE = 0x00008000,
    /// <summary>
    /// Allow folder junctions such as a library or a compressed file with a .zip file name extension to be browsed.
    /// </summary>
    BIF_BROWSEFILEJUNCTIONS = 0x00010000,
}
```

## VB.NET Definition:
```cs
<Flags> _
Public Enum BrowseInfoFlags As UInteger
    ''' <summary>
    ''' Only return file system directories. 
    ''' </summary>
    BIF_RETURNONLYFSDIRS = &H00000001
    ''' <summary>
    ''' Do not include network folders below the domain level in the dialog box's tree view control.
    ''' </summary>
    BIF_DONTGOBELOWDOMAIN = &H00000002
    ''' <summary>
    ''' Include a status area in the dialog box. 
    ''' The callback function can set the status text by sending messages to the dialog box. 
    ''' This flag is not supported when <bold>BIF_NEWDIALOGSTYLE</bold> is specified
    ''' </summary>
    BIF_STATUSTEXT = &H00000004
    ''' <summary>
    ''' Only return file system ancestors. 
    ''' An ancestor is a subfolder that is beneath the root folder in the namespace hierarchy. 
    ''' If the user selects an ancestor of the root folder that is not part of the file system, the OK button is grayed
    ''' </summary>
    BIF_RETURNFSANCESTORS = &H00000008
    ''' <summary>
    ''' Include an edit control in the browse dialog box that allows the user to type the name of an item.
    ''' </summary>
    BIF_EDITBOX = &H00000010
    ''' <summary>
    ''' If the user types an invalid name into the edit box, the browse dialog box calls the application's BrowseCallbackProc with the BFFM_VALIDATEFAILED message. 
    ''' This flag is ignored if <bold>BIF_EDITBOX</bold> is not specified.
    ''' </summary>
    BIF_VALIDATE = &H00000020
    ''' <summary>
    ''' Use the new user interface. 
    ''' Setting this flag provides the user with a larger dialog box that can be resized. 
    ''' The dialog box has several new capabilities, including: drag-and-drop capability within the 
    ''' dialog box, reordering, shortcut menus, new folders, delete, and other shortcut menu commands. 
    ''' </summary>
    BIF_NEWDIALOGSTYLE = &H00000040
    ''' <summary>
    ''' The browse dialog box can display URLs. The <bold>BIF_USENEWUI</bold> and <bold>BIF_BROWSEINCLUDEFILES</bold> flags must also be set. 
    ''' If any of these three flags are not set, the browser dialog box rejects URLs.
    ''' </summary>
    BIF_BROWSEINCLUDEURLS = &H00000080
    ''' <summary>
    ''' Use the new user interface, including an edit box. This flag is equivalent to <bold>BIF_EDITBOX | BIF_NEWDIALOGSTYLE</bold>
    ''' </summary>
    BIF_USENEWUI = (BIF_EDITBOX Or BIF_NEWDIALOGSTYLE)
    ''' <summary>
    ''' hen combined with <bold>BIF_NEWDIALOGSTYLE</bold>, adds a usage hint to the dialog box, in place of the edit box. <bold>BIF_EDITBOX</bold> overrides this flag.
    ''' </summary>
    BIF_UAHINT = &H00000100
    ''' <summary>
    ''' Do not include the New Folder button in the browse dialog box.
    ''' </summary>
    BIF_NONEWFOLDERBUTTON = &H00000200
    ''' <summary>
    ''' When the selected item is a shortcut, return the PIDL of the shortcut itself rather than its target.
    ''' </summary>
    BIF_NOTRANSLATETARGETS = &H00000400
    ''' <summary>
    ''' Only return computers. If the user selects anything other than a computer, the OK button is grayed.
    ''' </summary>
    BIF_BROWSEFORCOMPUTER = &H00001000
    ''' <summary>
    ''' Only allow the selection of printers. If the user selects anything other than a printer, the OK button is grayed
    ''' </summary>
    BIF_BROWSEFORPRINTER = &H00002000
    ''' <summary>
    ''' The browse dialog box displays files as well as folders.
    ''' </summary>
    BIF_BROWSEINCLUDEFILES = &H00004000
    ''' <summary>
    ''' The browse dialog box can display shareable resources on remote systems.
    ''' </summary>
    BIF_SHAREABLE = &H00008000
    ''' <summary>
    ''' Allow folder junctions such as a library or a compressed file with a .zip file name extension to be browsed.
    ''' </summary>
    BIF_BROWSEFILEJUNCTIONS = &H00010000
End Enum
```

## VB Definition
```cs
Public Enum BrowseInfoFlags
    BIF_RETURNONLYFSDIRS As Long = &H00000001
    BIF_DONTGOBELOWDOMAIN As Long = &H00000002
    BIF_STATUSTEXT As Long = &H00000004
    BIF_RETURNFSANCESTORS As Long = &H00000008
    BIF_EDITBOX As Long = &H00000010
    BIF_VALIDATE As Long = &H00000020
    BIF_NEWDIALOGSTYLE As Long = &H00000040
    BIF_BROWSEINCLUDEURLS As Long = &H00000080
    BIF_USENEWUI As Long = (BIF_EDITBOX Or BIF_NEWDIALOGSTYLE)
    BIF_UAHINT As Long = &H00000100
    BIF_NONEWFOLDERBUTTON As Long = &H00000200
    BIF_NOTRANSLATETARGETS As Long = &H00000400
    BIF_BROWSEFORCOMPUTER As Long = &H00001000
    BIF_BROWSEFORPRINTER As Long = &H00002000
    BIF_BROWSEINCLUDEFILES As Long = &H00004000
    BIF_SHAREABLE As Long = &H00008000
    BIF_BROWSEFILEJUNCTIONS As Long = &H00010000
End Enum
```
