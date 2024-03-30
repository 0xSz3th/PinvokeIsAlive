
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto)]
public struct OpenFileName
{
    public int lStructSize;
    public IntPtr hwndOwner;
    public IntPtr hInstance;
    public string lpstrFilter;
    public string lpstrCustomFilter;
    public int nMaxCustFilter;
    public int nFilterIndex;
    public string lpstrFile;
    public int nMaxFile;
    public string lpstrFileTitle;
    public int nMaxFileTitle;
    public string lpstrInitialDir;
    public string lpstrTitle;
    public int Flags;
    public short nFileOffset;
    public short nFileExtension;
    public string lpstrDefExt;
    public IntPtr lCustData;
    public IntPtr lpfnHook;
    public string lpTemplateName;
    public IntPtr pvReserved;
    public int dwReserved;
    public int flagsEx;
}
```

## VB.NET Definition:
```cs
Public Structure OpenFileName
    ''' <summary>
    ''' The length, in bytes, of the structure. Use sizeof (OPENFILENAME) for this parameter.
    ''' </summary>
    Public lStructSize As Integer
    ''' <summary>
    ''' A handle to the window that owns the dialog box. This member can be any valid window handle, or it can be NULL if the dialog box has no owner
    ''' </summary>
    Public hwndOwner As IntPtr  
    ''' <summary>
    ''' f the OFN_ENABLETEMPLATEHANDLE flag is set in the Flags member, 
    ''' hInstance is a handle to a memory object containing a dialog box template. 
    ''' If the OFN_ENABLETEMPLATE flag is set, 
    ''' hInstance is a handle to a module that contains a dialog box template named by the lpTemplateName member. 
    ''' If neither flag is set, this member is ignored. 
    ''' If the OFN_EXPLORER flag is set, 
    ''' the system uses the specified template to create a dialog box that is a child of the default Explorer-style dialog box. 
    ''' If the OFN_EXPLORER flag is not set, 
    ''' the system uses the template to create an old-style dialog box that replaces the default dialog box.
    ''' </summary>
    Public hInstance As IntPtr 
    ''' <summary>
    ''' A buffer containing pairs of null-terminated filter strings. The last string in the buffer must be terminated by two NULL characters.
    ''' </summary>
    <MarshalAs(UnmanagedType.LPTSTR)>Public lpstrFilter As String
    ''' <summary>
    ''' A static buffer that contains a pair of null-terminated filter strings for preserving 
    ''' the filter pattern chosen by the user. 
    ''' The first string is your display string that describes the custom filter, 
    ''' and the second string is the filter pattern selected by the user. 
    ''' 
    ''' The first time your application creates the dialog box, 
    ''' you specify the first string, which can be any nonempty string. 
    ''' 
    ''' When the user selects a file, the dialog box copies the current filter pattern 
    ''' to the second string. The preserved filter pattern can be one of the patterns 
    ''' specified in the lpstrFilter buffer, or it can be a filter pattern typed by the user. 
    ''' 
    ''' The system uses the strings to initialize the user-defined file filter the next time 
    ''' the dialog box is created. 
    ''' 
    ''' If the nFilterIndex member is zero, the dialog box uses the custom filter. 
    ''' </summary>
    <MarshalAs(UnmanagedType.LPTSTR)>Public lpstrCustomFilter As String
    ''' <summary>
    ''' The size, in characters, of the buffer identified by lpstrCustomFilter. 
    ''' This buffer should be at least 40 characters long. 
    ''' This member is ignored if lpstrCustomFilter is NULL or points to a NULL string.
    ''' </summary>
    Public nMaxCustFilter As Integer ' Ignored
    ''' <summary>
    ''' The index of the currently selected filter in the File Types control. 
    ''' The buffer pointed to by lpstrFilter contains pairs of strings that define the filters. 
    ''' 
    ''' The first pair of strings has an index value of 1, the second pair 2, and so on. 
    ''' 
    ''' An index of zero indicates the custom filter specified by lpstrCustomFilter. 
    ''' You can specify an index on input to indicate the initial filter description and filter 
    ''' pattern for the dialog box. 
    ''' 
    ''' When the user selects a file, nFilterIndex returns the index of the currently displayed 
    ''' filter. 
    ''' 
    ''' If nFilterIndex is zero and lpstrCustomFilter is NULL, the system uses the first 
    ''' filter in the lpstrFilter buffer. 
    ''' 
    ''' If all three members are zero or NULL, the system does not use any filters and does 
    ''' not show any files in the file list control of the dialog box.
    ''' </summary>
    Public nFilterIndex As Integer 
    ''' <summary>
    ''' The file name used to initialize the File Name edit control. 
    ''' The first character of this buffer must be NULL if initialization is not necessary. 
    ''' When the GetOpenFileName or GetSaveFileName function returns successfully, 
    ''' this buffer contains the drive designator, path, file name, and extension of the 
    ''' selected file.
    ''' </summary>
    <MarshalAs(UnmanagedType.LPTSTR)>Public lpstrFile As String 
    ''' <summary>
    ''' The size, in characters, of the buffer pointed to by lpstrFile. 
    ''' The buffer must be large enough to store the path and file name string or strings, 
    ''' including the terminating NULL character. 
    ''' The GetOpenFileName and GetSaveFileName functions return FALSE if the buffer is 
    ''' too small to contain the file information. 
    ''' The buffer should be at least 256 characters long.
    ''' </summary>
    Public nMaxFile As Integer ' Handled internally
    ''' <summary>
    ''' The file name and extension (without path information) of the selected file. This member can be NULL.
    ''' </summary>
    <MarshalAs(UnmanagedType.LPTSTR)>Public lpstrFileTitle As String 
    ''' <summary>
    ''' The size, in characters, of the buffer pointed to by lpstrFileTitle. This member is ignored if lpstrFileTitle is NULL.
    ''' </summary>
    Public nMaxFileTitle As Integer 
    ''' <summary>
    ''' The initial directory. The algorithm for selecting the initial directory varies on different platforms.
    ''' </summary>
    <MarshalAs(UnmanagedType.LPTSTR)>Public lpstrInitialDir As String
    ''' <summary>
    ''' A string to be placed in the title bar of the dialog box. If this member is NULL, the system uses the default title (that is, Save As or Open)
    ''' </summary>
    <MarshalAs(UnmanagedType.LPTSTR)>Public lpstrTitle As String
    ''' <summary>
    ''' A set of bit flags you can use to initialize the dialog box. 
    ''' When the dialog box returns, it sets these flags to indicate the user's input. 
    ''' This member can be a combination of the CommomDialgueFlags.
    ''' </summary>
    <MarshalAs(UnmanagedType.I4)>Public Flags As OpenSaveFileDialgueFlags
    ''' <summary>
    ''' he zero-based offset, in characters, from the beginning of the path to the file name 
    ''' in the string pointed to by lpstrFile. 
    ''' For the ANSI version, this is the number of bytes; for the Unicode version, 
    ''' this is the number of characters. 
    ''' 
    ''' For example, if lpstrFile points to the following string, 
    ''' "c:\dir1\dir2\file.ext", this member contains the value 13 to indicate the 
    ''' offset of the "file.ext" string. 
    ''' 
    ''' If the user selects more than one file, nFileOffset is the offset to the first file name.
    ''' </summary>
    Public nFileOffset As Short 
    ''' <summary>
    ''' The zero-based offset, in characters, from the beginning of the path to the file name extension in the string pointed to by lpstrFile. 
    ''' </summary>
    Public nFileExtension As Short
    ''' <summary>
    ''' The default extension. GetOpenFileName and GetSaveFileName append this extension to the file name if the user fails to type an extension. 
    ''' </summary>
    <MarshalAs(UnmanagedType.LPTSTR)>Public lpstrDefExt As String
    ''' <summary>
    ''' Application-defined data that the system passes to the hook procedure identified by the lpfnHook member.
    ''' </summary>
    Public lCustData As Integer 
    ''' <summary>
    ''' A pointer to a hook procedure. This member is ignored unless the Flags member includes the OFN_ENABLEHOOK flag.
    ''' </summary>
    <MarshalAs(UnmanagedType.FunctionPtr)>Public lpfnHook As IntPtr 
    ''' <summary>
    ''' The name of the dialog template resource in the module identified by the hInstance member.
    ''' </summary>
    Public lpTemplateName As Integer
End Structure
```

## VB Definition
```cs
Public Type OPENFILENAME
     StructSize As Long
     OwnerWindowHandle As Long
     OwnerAppHandle As Long
     filter As String
     CustomerFilter As String
     CustomFilterLen As Long
     FilterIndex As Long
     InitFileName As String
     InitFileNameLen As Long
     FileName As String
     FileNameLen As Long
     InitialDirectory As String
     DialogueTitle As String
     Flags As OpenSaveFileDialgueFlags
     FileOffset As Integer
     FileOffsetExtension As Integer
     DefaultExtension As String
     CustomData As Long
     HookData As Long
     TemplateName As String
End Type
```
