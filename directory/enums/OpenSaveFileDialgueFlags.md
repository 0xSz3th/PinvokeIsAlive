
## C# Definition:
```cs
[Flags] _
public enum OpenSaveFileDialgueFlags : int
{
    OFN_READONLY = 0x1
    OFN_OVERWRITEPROMPT = 0x2
    OFN_HIDEREADONLY = 0x4
    OFN_NOCHANGEDIR = 0x8
    OFN_SHOWHELP = 0x10
    OFN_ENABLEHOOK = 0x20
    OFN_ENABLETEMPLATE = 0x40
    OFN_ENABLETEMPLATEHANDLE = 0x80
    OFN_NOVALIDATE = 0x100
    OFN_ALLOWMULTISELECT = 0x200
    OFN_EXTENSIONDIFFERENT = 0x400
    OFN_PATHMUSTEXIST = 0x800
    OFN_FILEMUSTEXIST = 0x1000
    OFN_CREATEPROMPT = 0x2000
    OFN_SHAREAWARE = 0x4000
    OFN_NOREADONLYRETURN = 0x8000
    OFN_NOTESTFILECREATE = 0x10000
    OFN_NONETWORKBUTTON = 0x20000
    /// <summary>
    /// Force no long names for 4.x modules
    /// </summary>
    OFN_NOLONGNAMES = 0x40000
    /// <summary>
    /// New look commdlg
    /// </summary>
    OFN_EXPLORER = 0x80000
    OFN_NODEREFERENCELINKS = 0x100000
    /// <summary>
    /// Force long names for 3.x modules
    /// </summary>
    OFN_LONGNAMES = 0x200000
  }
```

## VB.NET Definition:
```cs
<Flags> _
Public Enum OpenSaveFileDialgueFlags As Integer
    OFN_READONLY = &H1
    OFN_OVERWRITEPROMPT = &H2
    OFN_HIDEREADONLY = &H4
    OFN_NOCHANGEDIR = &H8
    OFN_SHOWHELP = &H10
    OFN_ENABLEHOOK = &H20
    OFN_ENABLETEMPLATE = &H40
    OFN_ENABLETEMPLATEHANDLE = &H80
    OFN_NOVALIDATE = &H100
    OFN_ALLOWMULTISELECT = &H200
    OFN_EXTENSIONDIFFERENT = &H400
    OFN_PATHMUSTEXIST = &H800
    OFN_FILEMUSTEXIST = &H1000
    OFN_CREATEPROMPT = &H2000
    OFN_SHAREAWARE = &H4000
    OFN_NOREADONLYRETURN = &H8000
    OFN_NOTESTFILECREATE = &H10000
    OFN_NONETWORKBUTTON = &H20000
    ''' <summary>
    ''' Force no long names for 4.x modules
    ''' </summary>
    OFN_NOLONGNAMES = &H40000
    ''' <summary>
    ''' New look commdlg
    ''' </summary>
    OFN_EXPLORER = &H80000
    OFN_NODEREFERENCELINKS = &H100000
    ''' <summary>
    ''' Force long names for 3.x modules
    ''' </summary>
    OFN_LONGNAMES = &H200000
End Enum
```

## VB Definition:
```cs
Public Enum OpenSaveFileDialgueFlags 
    OFN_READONLY As Long = &H1
    OFN_OVERWRITEPROMPT As Long = &H2
    OFN_HIDEREADONLY As Long = &H4
    OFN_NOCHANGEDIR As Long = &H8
    OFN_SHOWHELP As Long = &H10
    OFN_ENABLEHOOK As Long = &H20
    OFN_ENABLETEMPLATE As Long = &H40
    OFN_ENABLETEMPLATEHANDLE As Long = &H80
    OFN_NOVALIDATE As Long = &H100
    OFN_ALLOWMULTISELECT As Long = &H200
    OFN_EXTENSIONDIFFERENT As Long = &H400
    OFN_PATHMUSTEXIST As Long = &H800
    OFN_FILEMUSTEXIST As Long = &H1000
    OFN_CREATEPROMPT As Long = &H2000
    OFN_SHAREAWARE As Long = &H4000
    OFN_NOREADONLYRETURN As Long = &H8000
    OFN_NOTESTFILECREATE As Long = &H10000
    OFN_NONETWORKBUTTON As Long = &H20000
    OFN_NOLONGNAMES As Long = &H40000
    OFN_EXPLORER As Long = &H80000
    OFN_NODEREFERENCELINKS As Long = &H100000
    OFN_LONGNAMES As Long = &H200000
End Enum
```
