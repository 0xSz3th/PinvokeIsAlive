
## C# Signature:
```cs
[DllImport("shell32.dll")]
static extern int SHGetFolderPath(IntPtr hwndOwner, int nFolder, IntPtr hToken,
   uint dwFlags, [Out] StringBuilder pszPath);
```

## VB.Net Signature:
```cs
<DllImport("shell32.dll")> _
    Private Shared Function SHGetFolderPath(ByVal hwndOwner As IntPtr, ByVal nFolder As Int32, ByVal hToken As IntPtr, ByVal dwFlags As Int32, ByVal pszPath As StringBuilder) As Int32
    End Function
```

## C# struct for nFolder:
```cs
public enum SpecialFolderType
    {
        // Version 5.0. The file system directory that is used 
        // to store administrative tools for an individual user. 
        // The Microsoft Management Console (MMC) will save customized 
        // consoles to this directory, and it will roam with the user.
        AdministrativeTools = 0x0030,

        // Version 5.0. The file system directory containing 
        // administrative tools for all users of the computer.
        CommonAdministrativeTools = 0x002f,

        // Version 4.71. The file system directory that serves as 
        // a common repository for application-specific data. 
        // A typical path is C:\Documents and Settings\username\Application Data. 
        // This CSIDL is supported by the redistributable Shfolder.dll 
        // for systems that do not have the Microsoft Internet Explorer 4.0 
        // integrated Shell installed
        ApplicationData = 0x001a,

        // Version 5.0. The file system directory containing 
        // application data for all users. A typical path is 
        // C:\Documents and Settings\All Users\Application Data.
        CommonAppData = 0x0023,

        // The file system directory that contains documents 
        // that are common to all users. A typical paths is 
        // C:\Documents and Settings\All Users\Documents. 
        // Valid for Windows NT systems and Microsoft Windows 95 and 
        // Windows 98 systems with Shfolder.dll installed.
        CommonDocuments = 0x002e,

        // The file system directory that serves as a common repository 
        // for Internet cookies. A typical path is 
        // C:\Documents and Settings\username\Cookies.
        Cookies = 0x0021,

        // Version 5.0. Combine this CSIDL with any of the following CSIDLs 
        // to force the creation of the associated folder. 
        CreateFlag = 0x8000,

        // The file system directory that serves as a common repository 
        // for Internet history items.
        History = 0x0022,

        // Version 4.72. The file system directory that serves as 
        // a common repository for temporary Internet files. A typical 
        // path is C:\Documents and Settings\username\Local Settings\Temporary Internet Files.
        InternetCache = 0x0020,

        // Version 5.0. The file system directory that serves as a data 
        // repository for local (nonroaming) applications. A typical path 
        // is C:\Documents and Settings\username\Local Settings\Application Data.
        LocalApplicationData = 0x001c,

        // Version 5.0. The file system directory that serves as 
        // a common repository for image files. A typical path is 
        // C:\Documents and Settings\username\My Documents\My Pictures.
        MyPictures = 0x0027,

        // Version 6.0. The virtual folder representing the My Documents 
        // desktop item. This is equivalent to CSIDL_MYDOCUMENTS. 
        // Previous to Version 6.0. The file system directory used to 
        // physically store a user's common repository of documents. 
        // A typical path is C:\Documents and Settings\username\My Documents. 
        // This should be distinguished from the virtual My Documents folder 
        // in the namespace. To access that virtual folder, 
        // use SHGetFolderLocation, which returns the ITEMIDLIST for the 
        // virtual location, or refer to the technique described in 
        // Managing the File System.
        Personal = 0x0005,

        // Version 5.0. The Program Files folder. A typical 
        // path is C:\Program Files.
        ProgramFiles = 0x0026,

        // Version 5.0. A folder for components that are shared across 
        // applications. A typical path is C:\Program Files\Common. 
        // Valid only for Windows NT, Windows 2000, and Windows XP systems. 
        // Not valid for Windows Millennium Edition (Windows Me).
        CommonProgramFiles = 0x002b,

        // Version 5.0. The Windows System folder. A typical 
        // path is C:\Windows\System32.
        System = 0x0025,

        // Version 5.0. The Windows directory or SYSROOT. 
        // This corresponds to the %windir% or %SYSTEMROOT% environment 
        // variables. A typical path is C:\Windows.
        Windows = 0x0024,

        // Fonts directory. A typical path is c:\Windows\Fonts.
        Fonts = 0x0014
    }
```

## Another C# Struct for nFolder:
```cs
public enum SpecialFolderCSIDL : int
    {
        CSIDL_DESKTOP         = 0x0000,    // <desktop>
        CSIDL_INTERNET        = 0x0001,    // Internet Explorer (icon on desktop)
        CSIDL_PROGRAMS        = 0x0002,    // Start Menu\Programs
        CSIDL_CONTROLS        = 0x0003,    // My Computer\Control Panel
        CSIDL_PRINTERS        = 0x0004,    // My Computer\Printers
        CSIDL_PERSONAL        = 0x0005,    // My Documents
        CSIDL_FAVORITES           = 0x0006,    // <user name>\Favorites
        CSIDL_STARTUP         = 0x0007,    // Start Menu\Programs\Startup
        CSIDL_RECENT          = 0x0008,    // <user name>\Recent
        CSIDL_SENDTO          = 0x0009,    // <user name>\SendTo
        CSIDL_BITBUCKET           = 0x000a,    // <desktop>\Recycle Bin
        CSIDL_STARTMENU           = 0x000b,    // <user name>\Start Menu
        CSIDL_DESKTOPDIRECTORY    = 0x0010,    // <user name>\Desktop
        CSIDL_DRIVES          = 0x0011,    // My Computer
        CSIDL_NETWORK         = 0x0012,    // Network Neighborhood
        CSIDL_NETHOOD         = 0x0013,    // <user name>\nethood
        CSIDL_FONTS           = 0x0014,    // windows\fonts
        CSIDL_TEMPLATES           = 0x0015,
        CSIDL_COMMON_STARTMENU    = 0x0016,    // All Users\Start Menu
        CSIDL_COMMON_PROGRAMS     = 0x0017,    // All Users\Programs
        CSIDL_COMMON_STARTUP      = 0x0018,    // All Users\Startup
        CSIDL_COMMON_DESKTOPDIRECTORY = 0x0019,    // All Users\Desktop
        CSIDL_APPDATA         = 0x001a,    // <user name>\Application Data
        CSIDL_PRINTHOOD           = 0x001b,    // <user name>\PrintHood
        CSIDL_LOCAL_APPDATA       = 0x001c,    // <user name>\Local Settings\Applicaiton Data (non roaming)
        CSIDL_ALTSTARTUP          = 0x001d,    // non localized startup
        CSIDL_COMMON_ALTSTARTUP       = 0x001e,    // non localized common startup
        CSIDL_COMMON_FAVORITES    = 0x001f,
        CSIDL_INTERNET_CACHE      = 0x0020,
        CSIDL_COOKIES         = 0x0021,
        CSIDL_HISTORY         = 0x0022,
        CSIDL_COMMON_APPDATA      = 0x0023,    // All Users\Application Data
        CSIDL_WINDOWS         = 0x0024,    // GetWindowsDirectory()
        CSIDL_SYSTEM          = 0x0025,    // GetSystemDirectory()
        CSIDL_PROGRAM_FILES       = 0x0026,    // C:\Program Files
        CSIDL_MYPICTURES          = 0x0027,    // C:\Program Files\My Pictures
        CSIDL_PROFILE         = 0x0028,    // USERPROFILE
        CSIDL_SYSTEMX86           = 0x0029,    // x86 system directory on RISC
        CSIDL_PROGRAM_FILESX86    = 0x002a,    // x86 C:\Program Files on RISC
        CSIDL_PROGRAM_FILES_COMMON    = 0x002b,    // C:\Program Files\Common
        CSIDL_PROGRAM_FILES_COMMONX86 = 0x002c,    // x86 Program Files\Common on RISC
        CSIDL_COMMON_TEMPLATES    = 0x002d,    // All Users\Templates
        CSIDL_COMMON_DOCUMENTS    = 0x002e,    // All Users\Documents
        CSIDL_COMMON_ADMINTOOLS       = 0x002f,    // All Users\Start Menu\Programs\Administrative Tools
        CSIDL_ADMINTOOLS          = 0x0030,    // <user name>\Start Menu\Programs\Administrative Tools
        CSIDL_CONNECTIONS         = 0x0031,    // Network and Dial-up Connections
        CSIDL_CDBURN_AREA         = 0x003B,    // Data for burning with interface ICDBurn

    };
```

## User-Defined Types:
```cs
Private Const CSIDL_WINDOWS As Integer = &H24
```

## Sample Code:
```cs
Dim winPath As New StringBuilder(300)
    If SHGetFolderPath(Nothing, CSIDL_WINDOWS, Nothing, 0, winPath) <> 0 Then
        Throw New ApplicationException("Can't get window's directory")
    End If
    Console.WriteLine(winPath.ToString)
```

## Sample Code C#:
```cs
const int MaxPath = 260;
    StringBuilder SB = new StringBuilder(MaxPath);
    SHGetFolderPath(IntPtr.Zero,0x0019,IntPtr.Zero,0x0000,SB);
    DesktopPath = SB.ToString();
```

##  Sample Code C#:
```cs
/// <summary>
    /// Gets the system fonts directory path.
    /// </summary>
    /// <returns>The fonts directory path</returns>
    private static String GetFontsDirectory()
    {
        const int MaxPath = 260;
        StringBuilder sb = new StringBuilder(MaxPath);
        int fontFolder = 0x0014;

        SHGetFolderPath(IntPtr.Zero, fontFolder, IntPtr.Zero, 0x0000, sb);
        return sb.ToString();
    }
```

## Sample Code C#:
```cs
/// <summary>
    /// Get the path to a special folder
    /// </summary>
    /// <param name="folder">The special folder's CSIDL enumeration</param>
    /// <returns>The full path of the special folder</returns>
    public static string GetSpecialFolder(SpecialFolderCSIDL folder)
    {
        const int MaxPath = 260;
        StringBuilder builder = new StringBuilder(MaxPath);
        SHGetFolderPath(IntPtr.Zero, (int)folder, IntPtr.Zero, 0x0000, builder);
        return builder.ToString();
    }
```

## Alternative Managed API:
```cs
Environment.GetFolderPath(Environment.SpecialFolder enumFolder)
```
