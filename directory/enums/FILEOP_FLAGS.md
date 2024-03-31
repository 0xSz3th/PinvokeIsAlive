
## C# Definition:
```cs
[Flags]
public enum FILEOP_FLAGS : ushort
{
    FOF_MULTIDESTFILES     = 0x1,
    FOF_CONFIRMMOUSE       = 0x2,
    /// <summary>
    /// Don't create progress/report
    /// </summary>
    FOF_SILENT         = 0x4,
    FOF_RENAMEONCOLLISION      = 0x8,
    /// <summary>
    /// Don't prompt the user.
    /// </summary>
    FOF_NOCONFIRMATION     = 0x10,    
    /// <summary>
    /// Fill in SHFILEOPSTRUCT.hNameMappings.
    /// Must be freed using SHFreeNameMappings
    /// </summary>
    FOF_WANTMAPPINGHANDLE      = 0x20,
    FOF_ALLOWUNDO          = 0x40,
    /// <summary>
    /// On *.*, do only files
    /// </summary>
    FOF_FILESONLY          = 0x80,
    /// <summary>
    /// Don't show names of files
    /// </summary>
    FOF_SIMPLEPROGRESS     = 0x100,
    /// <summary>
    /// Don't confirm making any needed dirs
    /// </summary>
    FOF_NOCONFIRMMKDIR     = 0x200,
    /// <summary>
    /// Don't put up error UI
    /// </summary>
    FOF_NOERRORUI          = 0x400,
    /// <summary>
    /// Dont copy NT file Security Attributes
    /// </summary>
    FOF_NOCOPYSECURITYATTRIBS  = 0x800,
    /// <summary>
    /// Don't recurse into directories.
    /// </summary>
    FOF_NORECURSION        = 0x1000,
    /// <summary>
    /// Don't operate on connected elements.
    /// </summary>
    FOF_NO_CONNECTED_ELEMENTS  = 0x2000,
    /// <summary>
    /// During delete operation, 
    /// warn if nuking instead of recycling (partially overrides FOF_NOCONFIRMATION)
    /// </summary>
    FOF_WANTNUKEWARNING    = 0x4000,
    /// <summary>
    /// Treat reparse points as objects, not containers
    /// </summary>
    FOF_NORECURSEREPARSE       = 0x8000
}
```

## VB.NET Definition:
```cs
<Flags> _
Public Enum FILEOP_FLAGS As UShort
    FOF_MULTIDESTFILES     = &H1
    FOF_CONFIRMMOUSE       = &H2
    ''' <summary>
    ''' Don't create progress/report
    ''' </summary>
    FOF_SILENT         = &H4     
    FOF_RENAMEONCOLLISION      = &H8
    ''' <summary>
    ''' Don't prompt the user.
    ''' </summary>
    FOF_NOCONFIRMATION     = &H10    
    ''' <summary>
    ''' Fill in SHFILEOPSTRUCT.hNameMappings.
    ''' Must be freed using SHFreeNameMappings
    ''' </summary>
    FOF_WANTMAPPINGHANDLE      = &H20
    FOF_ALLOWUNDO          = &H40
    ''' <summary>
    ''' On *.*, do only files
    ''' </summary>
    FOF_FILESONLY          = &H80    
    ''' <summary>
    ''' Don't show names of files
    ''' </summary>
    FOF_SIMPLEPROGRESS     = &H100   
    ''' <summary>
    ''' Don't confirm making any needed dirs
    ''' </summary>
    FOF_NOCONFIRMMKDIR     = &H200
    ''' <summary>
    ''' Don't put up error UI
    ''' </summary>
    FOF_NOERRORUI          = &H400
    ''' <summary>
    ''' Dont copy NT file Security Attributes
    ''' </summary>
    FOF_NOCOPYSECURITYATTRIBS  = &H800
    ''' <summary>
    ''' Don't recurse into directories.
    ''' </summary>
    FOF_NORECURSION        = &H1000
    ''' <summary>
    ''' Don't operate on connected elements.
    ''' </summary>
    FOF_NO_CONNECTED_ELEMENTS  = &H2000
    ''' <summary>
    ''' During delete operation, 
    ''' warn if nuking instead of recycling (partially overrides FOF_NOCONFIRMATION)
    ''' </summary>
    FOF_WANTNUKEWARNING    = &H4000
    ''' <summary>
    ''' Treat reparse points as objects, not containers
    ''' </summary>
    FOF_NORECURSEREPARSE       = &H8000
End Enum
```

## VB Signature
```cs
Public Enum FILEOP_FLAGS
    FOF_MULTIDESTFILES     As Integer = &H1
    FOF_CONFIRMMOUSE       As Integer = &H2
    FOF_SILENT     As Integer = &H4    
    FOF_RENAMEONCOLLISION      As Integer = &H8
    FOF_NOCONFIRMATION     As Integer = &H10    
    FOF_WANTMAPPINGHANDLE      As Integer = &H20
    FOF_ALLOWUNDO      As Integer = &H40
    FOF_FILESONLY      As Integer = &H80    
    FOF_SIMPLEPROGRESS     As Integer = &H100  
    FOF_NOCONFIRMMKDIR     As Integer = &H200
    FOF_NOERRORUI      As Integer = &H400
    FOF_NOCOPYSECURITYATTRIBS  As Integer = &H800
    FOF_NORECURSION    As Integer = &H1000
    FOF_NO_CONNECTED_ELEMENTS  As Integer = &H2000
    FOF_WANTNUKEWARNING    As Integer = &H4000
    FOF_NORECURSEREPARSE       As Integer = &H8000
End Enum
```
