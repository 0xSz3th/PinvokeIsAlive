
## C# Constants:
```cs
public const int ABM_NEW        = 0x00000000;
    public const int ABM_REMOVE         = 0x00000001;
    public const int ABM_QUERYPOS       = 0x00000002;
    public const int ABM_SETPOS         = 0x00000003;
    public const int ABM_GETSTATE       = 0x00000004;
    public const int ABM_GETTASKBARPOS      = 0x00000005;
    public const int ABM_ACTIVATE       = 0x00000006; // lParam == TRUE/FALSE means activate/deactivate
    public const int ABM_GETAUTOHIDEBAR     = 0x00000007;
    public const int ABM_SETAUTOHIDEBAR     = 0x00000008; // this can fail at any time.  MUST check the result
    // lParam = TRUE/FALSE  Set/Unset
    // uEdge = what edge
    public const int ABM_WINDOWPOSCHANGED   = 0x0000009;
    public const int ABM_SETSTATE       = 0x0000000a;

    // these are put in the wparam of callback messages
    public const int ABN_STATECHANGE   = 0x0000000;
    public const int ABN_POSCHANGED    = 0x0000001;
    public const int ABN_FULLSCREENAPP = 0x0000002;
    public const int ABN_WINDOWARRANGE = 0x0000003; // lParam == TRUE means hide

    // flags for get state
    public const int ABS_AUTOHIDE    = 0x0000001;
    public const int ABS_ALWAYSONTOP = 0x0000002;

    public const int ABE_LEFT   = 0;
    public const int ABE_TOP    = 1;
    public const int ABE_RIGHT  = 2;
    public const int ABE_BOTTOM = 3;

    public const int FO_MOVE   = 0x0001;
    public const int FO_COPY   = 0x0002;
    public const int FO_DELETE = 0x0003;
    public const int FO_RENAME = 0x0004;

    public const int FOF_MULTIDESTFILES     = 0x0001;
    public const int FOF_CONFIRMMOUSE       = 0x0002;
    public const int FOF_SILENT         = 0x0004;  // don't create progress/report
    public const int FOF_RENAMEONCOLLISION      = 0x0008;
    public const int FOF_NOCONFIRMATION     = 0x0010;  // Don't prompt the user.
    public const int FOF_WANTMAPPINGHANDLE      = 0x0020;  // Fill in SHFILEOPSTRUCT.hNameMappings
        // Must be freed using SHFreeNameMappings
    public const int FOF_ALLOWUNDO          = 0x0040;
    public const int FOF_FILESONLY          = 0x0080;  // on *.*, do only files
    public const int FOF_SIMPLEPROGRESS     = 0x0100;  // means don't show names of files
    public const int FOF_NOCONFIRMMKDIR     = 0x0200;  // don't confirm making any needed dirs
    public const int FOF_NOERRORUI          = 0x0400;  // don't put up error UI
    public const int FOF_NOCOPYSECURITYATTRIBS  = 0x0800;  // dont copy NT file Security Attributes
    public const int FOF_NORECURSION        = 0x1000;  // don't recurse into directories.

        // #if (_WIN32_IE >= 0x0500)
    public const int FOF_NO_CONNECTED_ELEMENTS  = 0x2000;  // don't operate on connected elements.
    public const int FOF_WANTNUKEWARNING    = 0x4000;  // during delete operation, warn if nuking instead of recycling (partially overrides FOF_NOCONFIRMATION)
    // #endif // (_WIN32_IE >= 0x500)
    // #if (_WIN32_WINNT >= 0x0501)
    public const int FOF_NORECURSEREPARSE       = 0x8000;  // treat reparse points as objects, not containers
    // #endif // (_WIN32_WINNT >= 0x501)

    public const int PO_DELETE      = 0x0013;  // printer is being deleted
    public const int PO_RENAME      = 0x0014;  // printer is being renamed
    public const int PO_PORTCHANGE  = 0x0020;  // port this printer connected to is being changed
        // if this id is set, the strings received by
        // the copyhook are a doubly-null terminated
        // list of strings.  The first is the printer
        // name and the second is the printer port.
    public const int PO_REN_PORT    = 0x0034;  // PO_RENAME and PO_PORTCHANGE at same time.
```

## C# Constants:
```cs
/* regular WinExec() codes */
    public const int SE_ERR_FNF         = 2;       // file not found
    public const int SE_ERR_PNF         = 3;       // path not found
    public const int SE_ERR_ACCESSDENIED    = 5;       // access denied
    public const int SE_ERR_OOM         = 8;       // out of memory
    public const int SE_ERR_DLLNOTFOUND     = 32;

        /* error values for ShellExecute() beyond the regular WinExec() codes */
    public const int SE_ERR_SHARE       = 26;
    public const int SE_ERR_ASSOCINCOMPLETE = 27;
    public const int SE_ERR_DDETIMEOUT      = 28;
    public const int SE_ERR_DDEFAIL     = 29;
    public const int SE_ERR_DDEBUSY     = 30;
    public const int SE_ERR_NOASSOC     = 31;

    // Note CLASSKEY overrides CLASSNAME
    public const int SEE_MASK_CLASSNAME     = 0x00000001;
    public const int SEE_MASK_CLASSKEY      = 0x00000003;
    // Note INVOKEIDLIST overrides IDLIST
    public const int SEE_MASK_IDLIST        = 0x00000004;
    public const int SEE_MASK_INVOKEIDLIST      = 0x0000000c;
    public const int SEE_MASK_ICON          = 0x00000010;
    public const int SEE_MASK_HOTKEY        = 0x00000020;
    public const int SEE_MASK_NOCLOSEPROCESS    = 0x00000040;
    public const int SEE_MASK_CONNECTNETDRV     = 0x00000080;
    public const int SEE_MASK_FLAG_DDEWAIT      = 0x00000100;
    public const int SEE_MASK_DOENVSUBST    = 0x00000200;
    public const int SEE_MASK_FLAG_NO_UI    = 0x00000400;
    public const int SEE_MASK_UNICODE       = 0x00004000;
    public const int SEE_MASK_NO_CONSOLE    = 0x00008000;
    public const int SEE_MASK_ASYNCOK       = 0x00100000;
    public const int SEE_MASK_HMONITOR      = 0x00200000;
    // #if (_WIN32_IE >= 0x0560)
    public const int SEE_MASK_NOZONECHECKS      = 0x00800000;
    // #endif // (_WIN32_IE >= 0x560)
    // #if (_WIN32_IE >= 0x0500)
    public const int SEE_MASK_NOQUERYCLASSSTORE = 0x01000000;
    public const int SEE_MASK_WAITFORINPUTIDLE  = 0x02000000;
    // #endif // (_WIN32_IE >= 0x500)
    // #if (_WIN32_IE >= 0x0560)
    public const int SEE_MASK_FLAG_LOG_USAGE    = 0x04000000;
    // #endif // (_WIN32_IE >= 0x560)
```

## C# Constants:
```cs
// flags for SHEmptyRecycleBin
        //
    public const int SHERB_NOCONFIRMATION = 0x00000001;
    public const int SHERB_NOPROGRESSUI   = 0x00000002;
    public const int SHERB_NOSOUND    = 0x00000004;
```

## C# Constants:
```cs
// #if (_WIN32_IE >= 0x0500)
    public const int NIN_SELECT         = (WM_USER + 0);
    public const int NINF_KEY           = 0x1;
    public const int NIN_KEYSELECT      = (NIN_SELECT | NINF_KEY);
    // #endif

    // #if (_WIN32_IE >= 0x0501)
    public const int NIN_BALLOONSHOW    = (WM_USER + 2);
    public const int NIN_BALLOONHIDE    = (WM_USER + 3);
    public const int NIN_BALLOONTIMEOUT     = (WM_USER + 4);
    public const int NIN_BALLOONUSERCLICK   = (WM_USER + 5);
    // #endif
```

## C# Constants:
```cs
public const int NIM_ADD        = 0x00000000;
    public const int NIM_MODIFY         = 0x00000001;
    public const int NIM_DELETE         = 0x00000002;
    // #if (_WIN32_IE >= 0x0500)
    public const int NIM_SETFOCUS       = 0x00000003;
    public const int NIM_SETVERSION     = 0x00000004;
    public const int NOTIFYICON_VERSION     = 3;
    // #endif

    public const int NIF_MESSAGE        = 0x00000001;
    public const int NIF_ICON           = 0x00000002;
    public const int NIF_TIP        = 0x00000004;
    // #if (_WIN32_IE >= 0x0500)
    public const int NIF_STATE          = 0x00000008;
    public const int NIF_INFO           = 0x00000010;
    // #endif
    // #if (_WIN32_IE >= 0x600)
    public const int NIF_GUID           = 0x00000020;
    // #endif

    // #if (_WIN32_IE >= 0x0500)
    public const int NIS_HIDDEN         = 0x00000001;
    public const int NIS_SHAREDICON     = 0x00000002;

    // says this is the source of a shared icon

    // Notify Icon Infotip flags
    public const int NIIF_NONE      = 0x00000000;
    // icon flags are mutually exclusive
    // and take only the lowest 2 bits
    public const int NIIF_INFO      = 0x00000001;
    public const int NIIF_WARNING   = 0x00000002;
    public const int NIIF_ERROR     = 0x00000003;
    public const int NIIF_ICON_MASK = 0x0000000F;
    // #if (_WIN32_IE >= 0x0501)
    public const int NIIF_NOSOUND   = 0x00000010;
    // #endif
    // #endif
```

## C# Constants:
```cs
public const int SHGFI_ICON          = 0x000000100;     // get icon
    public const int SHGFI_DISPLAYNAME       = 0x000000200;     // get display name
    public const int SHGFI_TYPENAME      = 0x000000400;     // get type name
    public const int SHGFI_ATTRIBUTES    = 0x000000800;     // get attributes
    public const int SHGFI_ICONLOCATION      = 0x000001000;     // get icon location
    public const int SHGFI_EXETYPE       = 0x000002000;     // return exe type
    public const int SHGFI_SYSICONINDEX      = 0x000004000;     // get system icon index
    public const int SHGFI_LINKOVERLAY       = 0x000008000;     // put a link overlay on icon
    public const int SHGFI_SELECTED      = 0x000010000;     // show icon in selected state
    public const int SHGFI_ATTR_SPECIFIED    = 0x000020000;     // get only specified attributes
    public const int SHGFI_LARGEICON     = 0x000000000;     // get large icon
    public const int SHGFI_SMALLICON     = 0x000000001;     // get small icon
    public const int SHGFI_OPENICON      = 0x000000002;     // get open icon
    public const int SHGFI_SHELLICONSIZE     = 0x000000004;     // get shell size icon
    public const int SHGFI_PIDL          = 0x000000008;     // pszPath is a pidl
    public const int SHGFI_USEFILEATTRIBUTES = 0x000000010;     // use passed dwFileAttribute

    // #if (_WIN32_IE >= 0x0500)
    public const int SHGFI_ADDOVERLAYS       = 0x000000020;     // apply the appropriate overlays
    public const int SHGFI_OVERLAYINDEX      = 0x000000040;     // Get the index of the overlay
    // in the upper 8 bits of the iIcon
    // #endif

    public const int SHGNLI_PIDL       = 0x000000001;     // pszLinkTo is a pidl
    public const int SHGNLI_PREFIXNAME = 0x000000002;     // Make name "Shortcut to xxx"
    public const int SHGNLI_NOUNIQUE   = 0x000000004;     // don't do the unique name generation
    // #if (_WIN32_IE >= 0x0501)
    public const int SHGNLI_NOLNK      = 0x000000008;     // don't add ".lnk" extension
    // #endif // _WIN2_IE >= 0x0501

    // Printer stuff
    public const int PRINTACTION_OPEN         = 0;
    public const int PRINTACTION_PROPERTIES       = 1;
    public const int PRINTACTION_NETINSTALL       = 2;
    public const int PRINTACTION_NETINSTALLLINK   = 3;
    public const int PRINTACTION_TESTPAGE     = 4;
    public const int PRINTACTION_OPENNETPRN       = 5;
    public const int PRINTACTION_DOCUMENTDEFAULTS = 6;
    public const int PRINTACTION_SERVERPROPERTIES = 7;
```

## C# Constants:
```cs
public const int OFFLINE_STATUS_LOCAL      = 0x0001;    // If open, it's open locally
    public const int OFFLINE_STATUS_REMOTE     = 0x0002;    // If open, it's open remotely
    public const int OFFLINE_STATUS_INCOMPLETE = 0x0004;    // The local copy is currently imcomplete.
                                // The file will not be available offline
                                // until it has been synchronized.

    public const int SHIL_LARGE      = 0;   // normally 32x32
    public const int SHIL_SMALL      = 1;   // normally 16x16
    public const int SHIL_EXTRALARGE = 2;
    public const int SHIL_SYSSMALL   = 3;   // like SHIL_SMALL, but tracks system small icon metric correctly
    public const int SHIL_LAST       = SHIL_SYSSMALL;
```

## VB Constants:
```cs
TODO
```
