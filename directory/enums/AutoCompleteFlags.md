
## C# Definition:
```cs
[Flags]
enum AutoCompleteFlags : uint {
    SHACF_DEFAULT           = 0x00000000,  // Currently (SHACF_FILESYSTEM | SHACF_URLALL)
    SHACF_FILESYSTEM        = 0x00000001,  // This includes the File System as well as the rest of the shell (Desktop\My Computer\Control Panel\)
    SHACF_URLALL            = (SHACF_URLHISTORY | SHACF_URLMRU),
    SHACF_URLHISTORY        = 0x00000002,  // URLs in the User's History.
    SHACF_URLMRU            = 0x00000004,  // URLs in the User's Recently Used list.
    SHACF_USETAB            = 0x00000008,  // Use the tab to move thru the autocomplete possibilities instead of to the next dialog/window control.
    SHACF_FILESYS_ONLY          = 0x00000010,  // This includes the File System
    SHACF_FILESYS_DIRS          = 0x00000020,  // Same as SHACF_FILESYS_ONLY except it only includes directories, UNC servers, and UNC server shares.
    SHACF_AUTOSUGGEST_FORCE_ON      = 0x10000000,  // Ignore the registry default and force the feature on.
    SHACF_AUTOSUGGEST_FORCE_OFF     = 0x20000000,  // Ignore the registry default and force the feature off.
    SHACF_AUTOAPPEND_FORCE_ON       = 0x40000000,  // Ignore the registry default and force the feature on. (Also know as AutoComplete)
    SHACF_AUTOAPPEND_FORCE_OFF      = 0x80000000,  // Ignore the registry default and force the feature off. (Also know as AutoComplete)
}
```

## VB Definition:
```cs
<Flags()> _
Enum AutoCompleteFlags As Integer
    SHACF_DEFAULT = &H0     ' Currently (SHACF_FILESYSTEM | SHACF_URLALL)
    SHACF_FILESYSTEM = &H1      ' This includes the File System as well as the rest of the shell (Desktop\My Computer\Control Panel\)
    SHACF_URLALL = (SHACF_URLHISTORY Or SHACF_URLMRU)
    SHACF_URLHISTORY = &H2      ' URLs in the User's History
    SHACF_URLMRU = &H4      ' URLs in the User's Recently Used list.
    SHACF_USETAB = &H8      ' Use the tab to move thru the autocomplete possibilities instead of to the next dialog/window control.
    SHACF_FILESYS_ONLY = &H10   ' This includes the File System
    SHACF_FILESYS_DIRS = &H20   ' Same as SHACF_FILESYS_ONLY except it only includes directories, UNC servers, and UNC server shares.
    SHACF_AUTOSUGGEST_FORCE_ON = &H10000000       ' Ignore the registry default and force the feature on.
    SHACF_AUTOSUGGEST_FORCE_OFF = &H20000000      ' Ignore the registry default and force the feature off.
    SHACF_AUTOAPPEND_FORCE_ON = &H40000000    ' Ignore the registry default and force the feature on. (Also know as AutoComplete)
    SHACF_AUTOAPPEND_FORCE_OFF = &H80000000       ' Ignore the registry default and force the feature off. (Also know as AutoComplete)
End Enum
```
