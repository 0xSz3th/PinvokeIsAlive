
## C# Signature:
```cs
[DllImport("shell32.dll", SetLastError=true)]
static extern TODO SHGetNameFromIDList(TODO);
```

## C# Signature:
```cs
<System.Runtime.InteropServices.InAttribute()> _
   ByVal pidl As System.IntPtr, _
   ByVal sigdnName As SIGDN, _
   ByRef ppszName As System.IntPtr) As Integer
```

## Tips & Tricks:
```cs
ADMINTOOLS = &H30
    ALTSTARTUP = &H1D
    APPDATA = &H1A
    BITBUCKET = &HA
    CDBURN_AREA = &H3B
    COMMON_ADMINTOOLS = &H2F
    COMMON_ALTSTARTUP = &H1E
    COMMON_APPDATA = &H23
    COMMON_DESKTOPDIRECTORY = &H19
    COMMON_DOCUMENTS = &H2E
    COMMON_FAVORITES = &H1F
    COMMON_MUSIC = &H35
    COMMON_OEM_LINKS = &H3A
    COMMON_PICTURES = &H36
    COMMON_PROGRAMS = &H17
    COMMON_STARTMENU = &H16
    COMMON_STARTUP = &H18
    COMMON_TEMPLATES = &H2D
    COMMON_VIDEO = &H37
    COMPUTERSNEARME = &H3D
    CONNECTIONS = &H31
    CONTROLS = &H3
    COOKIES = &H21
    DESKTOP = &H0
    DESKTOPDIRECTORY = &H10
    DRIVES = &H11
    FAVORITES = &H6
    FLAG_CREATE = &H8000
    FLAG_DONT_VERIFY = &H4000
    FLAG_MASK = &HFF00
    FLAG_NO_ALIAS = &H1000
    FLAG_PER_USER_INIT = &H800
    FONTS = &H14
    HISTORY = &H22
    INTERNET = &H1
    INTERNET_CACHE = &H20
    LOCAL_APPDATA = &H1C
    MYDOCUMENTS = PERSONAL '&H5'  &HC
    MYMUSIC = &HD
    MYPICTURES = &H27
    MYVIDEO = &HE
    NETHOOD = &H13
    NETWORK = &H12
    PERSONAL = &H5
    PRINTERS = &H4
    PRINTHOOD = &H1B
    PROFILE = &H28
    PROGRAM_FILES = &H26
    PROGRAM_FILES_COMMON = &H2B
    PROGRAM_FILES_COMMONX86 = &H2C
    PROGRAM_FILESX86 = &H2A
    PROGRAMS = &H2
    RECENT = &H8
    RESOURCES = &H38
    RESOURCES_LOCALIZED = &H39
    SENDTO = &H9
    STARTMENU = &HB
    STARTUP = &H7
    SYSTEM = &H25
    SYSTEMX86 = &H29
    TEMPLATES = &H15
    WINDOWS = &H24
```

## Tips & Tricks:
```cs
CANCOPY = &H1                 '   Objects can be copied    (DROPEFFECT_COPY)
    CANMOVE = &H2                 '   Objects can be moved     (DROPEFFECT_MOVE)
    CANLINK = &H4                 '   Objects can be linked    (DROPEFFECT_LINK)
    STORAGE = &H8          '   supports BindToObject(IID_IStorage)
    CANRENAME = &H10         '   Objects can be renamed
    CANDELETE = &H20         '   Objects can be deleted
    HASPROPSHEET = &H40            '   Objects have property sheets
    DROPTARGET = &H100           '   Objects are drop target
    CAPABILITYMASK = &H177
     SYSTEM= &H1000  ' Windows 7 and later. The specified items are system items.
    ENCRYPTED = &H2000           '   object is encrypted (use alt color)
    ISSLOW = &H4000            '   'slow' object
    GHOSTED = &H8000         '   ghosted icon
    LINK = &H10000           '   Shortcut (link)
    SHARE = &H20000            '   shared
    [READONLY] = &H40000         '   read-only
    HIDDEN = &H80000         '   hidden object
    DISPLAYATTRMASK = &HFC000
    FILESYSANCESTOR = &H10000000         '   may contain children with FILESYSTEM
    FOLDER = &H20000000            '   support BindToObject(IID_IShellFolder)
    FILESYSTEM = &H40000000            '   is a win32 file system object (file/folder/root)
    HASSUBFOLDER = &H80000000UI          '   may contain children with FOLDER
    CONTENTSMASK = &H80000000UI
    VALIDATE = &H1000000         '   invalidate cached information
    REMOVABLE = &H2000000          '   is this removeable media?
    COMPRESSED = &H4000000           '   Object is compressed (use alt color)
    BROWSABLE = &H8000000          '   supports IShellFolder, but only implements CreateViewObject() (non-folder view)
    NONENUMERATED = &H100000         '   is a non-enumerated object
    NEWCONTENT = &H200000          '   should show bold in explorer tree
    CANMONIKER = &H400000          '   defunct
    HASSTORAGE = &H400000          '   defunct
    STREAM = &H400000          '   supports BindToObject(IID_IStream)
    STORAGEANCESTOR = &H800000           '   may contain children with STORAGE or STREAM
    STORAGECAPMASK = &H70C50008            '   for determining storage capabilities, ie for open/save semantics
```

## Tips & Tricks:
```cs
ICON = &H100
    DISPLAYNAME = &H200
    TYPENAME = &H400
    ATTRIBUTES = &H800
    ICONLOCATION = &H1000
    EXETYPE = &H2000
    SYSICONINDEX = &H4000
    LINKOVERLAY = &H8000
    SELECTED = &H10000
    ATTR_SPECIFIED = &H20000
    LARGEICON = &H0
    SMALLICON = &H1
    OPENICON = &H2
    SHELLICONSIZE = &H4
    PIDL = &H8
    USEFILEATTRIBUTES = &H10
    ADDOVERLAYS = &H20
    OVERLAYINDEX = &H40
```

## Tips & Tricks:
```cs
NORMALDISPLAY = 0
    PARENTRELATIVEPARSING = &H80018001UI
    PARENTRELATIVEFORADDRESSBAR = &H8001C001UI
    DESKTOPABSOLUTEPARSING = &H80028000UI
    PARENTRELATIVEEDITING = &H80031001UI
    DESKTOPABSOLUTEEDITING = &H8004C000UI
    FILESYSPATH = &H80058000UI
    URL = &H80068000UI
```

## Tips & Tricks:
```cs
<System.Runtime.InteropServices.DllImportAttribute("shell32.dll", EntryPoint:="ILFree")> _
    Private Shared Sub ILFree(<System.Runtime.InteropServices.InAttribute()> ByVal pidl As System.IntPtr)
    End Sub
```

## Tips & Tricks:
```cs
<System.Runtime.InteropServices.DllImportAttribute("shell32.dll", EntryPoint:="SHGetNameFromIDList")> _
    Private Shared Function SHGetNameFromIDList( _
   <System.Runtime.InteropServices.InAttribute()> _
   ByVal pidl As System.IntPtr, _
   ByVal sigdnName As SIGDN, _
   ByRef ppszName As System.IntPtr) As Integer
    End Function

    <System.Runtime.InteropServices.DllImportAttribute("shell32.dll", EntryPoint:="SHParseDisplayName")> _
    Private Shared Function SHParseDisplayName( _
```

## Tips & Tricks:
```cs
System.Runtime.InteropServices.UnmanagedType.LPWStr)> _
```

## Tips & Tricks:
```cs
End Function

    <DllImport("shell32.dll")>
    Private Shared Function SHGetFolderLocation(hwndOwner As IntPtr, nFolder As Integer,
   hToken As IntPtr, dwReserved As UInteger, ByRef ppidl As IntPtr) As Integer
    End Function
```

## Tips & Tricks:
```cs
Public Shared Function GetNameFromPIDL(pidl As IntPtr, _
       displayType As SIGDN) As String
        Dim ptr As IntPtr = Marshal.AllocHGlobal(300)
        SHGetNameFromIDList(pidl, displayType, ptr)
        Dim path As String = Marshal.PtrToStringAuto(ptr)
        Marshal.FreeHGlobal(ptr)
        Return path
    End Function
```

## Tips & Tricks:
```cs
Private Function PIDLFromCSIDL(csidlInt As Integer) As IntPtr
        If Not [Enum].IsDefined(GetType(CSIDL), csidlInt) Then Return IntPtr.Zero
        Dim ptr As IntPtr = IntPtr.Zero
        SHGetFolderLocation(IntPtr.Zero, CInt(csidlInt), IntPtr.Zero, 0, ptr)
        Return ptr
    End Function

    Private Function PIDLFromParseName(parseName As String) As IntPtr
        Dim ptr As IntPtr = IntPtr.Zero
        SHParseDisplayName(parseName, IntPtr.Zero, ptr, 0, 0)
        Return ptr
    End Function

    'Example = Get ParseName for Control Panel
    Public Function ControlPanelParseName() As String
        Dim CplCsidl As CSIDL = CSIDL.CONTROLS
        Dim ptrLoc As IntPtr = IntPtr.Zero
        SHGetFolderLocation(IntPtr.Zero, CInt(CplCsidl), IntPtr.Zero, 0, ptrLoc)
        Dim parseName As String = GetNameFromPIDL(ptrLoc, SIGDN.DESKTOPABSOLUTEPARSING)
        ILFree(ptrLoc)
        Return parseName
    End Function

    'Example = Get Display Name for 'My Computer'
    Public Function ComputerDisplayName() As String
        Dim pcCsidl As CSIDL = CSIDL.DRIVES
        Dim ptrLoc As IntPtr = IntPtr.Zero
        SHGetFolderLocation(IntPtr.Zero, CInt(pcCsidl), IntPtr.Zero, 0, ptrLoc)
        Dim displayName As String = GetNameFromPIDL(ptrLoc, SIGDN.NORMALDISPLAY)
        ILFree(ptrLoc)
        Return displayName
    End Function
```
