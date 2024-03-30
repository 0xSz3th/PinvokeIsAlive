
## C# Signature::
```cs
[DllImport("shell32.dll", CharSet = CharSet.Auto)]
static extern bool ShellExecuteEx(ref SHELLEXECUTEINFO lpExecInfo);
```

## VB.NET Signature:
```cs
<DllImport("Shell32", CharSet:=CharSet.Auto, SetLastError:=True)> _
Public Function ShellExecuteEx(ByRef lpExecInfo As SHELLEXECUTEINFO) As Boolean
End Function
```

## User-Defined Types:
```cs
Public Structure SHELLEXECUTEINFO
    Public cbSize As Integer
    Public fMask As Integer
    Public hwnd As IntPtr
    <MarshalAs(UnmanagedType.LPTStr)> Public lpVerb As String
    <MarshalAs(UnmanagedType.LPTStr)> Public lpFile As String
    <MarshalAs(UnmanagedType.LPTStr)> Public lpParameters As String
    <MarshalAs(UnmanagedType.LPTStr)> Public lpDirectory As String
    Dim nShow As Integer
    Dim hInstApp As IntPtr
    Dim lpIDList As IntPtr
    <MarshalAs(UnmanagedType.LPTStr)> Public lpClass As String
    Public hkeyClass As IntPtr
    Public dwHotKey As Integer
    Public hIcon As IntPtr
    Public hProcess As IntPtr
End Structure
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct SHELLEXECUTEINFO
    {
        public int cbSize;
        public uint fMask;
        public IntPtr hwnd;
        [MarshalAs(UnmanagedType.LPTStr)]
        public string lpVerb;
        [MarshalAs(UnmanagedType.LPTStr)]
        public string lpFile;
        [MarshalAs(UnmanagedType.LPTStr)]
        public string lpParameters;
        [MarshalAs(UnmanagedType.LPTStr)]
        public string lpDirectory;
        public int nShow;
        public IntPtr hInstApp;
        public IntPtr lpIDList;
        [MarshalAs(UnmanagedType.LPTStr)]
        public string lpClass;
        public IntPtr hkeyClass;
        public uint dwHotKey;
        public IntPtr hIcon;
        public IntPtr hProcess;
    }

    public enum ShowCommands : int
    {
        SW_HIDE = 0,
        SW_SHOWNORMAL = 1,
        SW_NORMAL = 1,
        SW_SHOWMINIMIZED = 2,
        SW_SHOWMAXIMIZED = 3,
        SW_MAXIMIZE = 3,
        SW_SHOWNOACTIVATE = 4,
        SW_SHOW = 5,
        SW_MINIMIZE = 6,
        SW_SHOWMINNOACTIVE = 7,
        SW_SHOWNA = 8,
        SW_RESTORE = 9,
        SW_SHOWDEFAULT = 10,
        SW_FORCEMINIMIZE = 11,
        SW_MAX = 11
    }

    [Flags]
    public enum ShellExecuteMaskFlags : uint
    {
        SEE_MASK_DEFAULT = 0x00000000,
        SEE_MASK_CLASSNAME = 0x00000001,  
        SEE_MASK_CLASSKEY = 0x00000003,   
        SEE_MASK_IDLIST = 0x00000004,   
        SEE_MASK_INVOKEIDLIST = 0x0000000c,   // Note SEE_MASK_INVOKEIDLIST(0xC) implies SEE_MASK_IDLIST(0x04) 
        SEE_MASK_HOTKEY = 0x00000020,   
        SEE_MASK_NOCLOSEPROCESS = 0x00000040, 
        SEE_MASK_CONNECTNETDRV = 0x00000080,  
        SEE_MASK_NOASYNC = 0x00000100,   
        SEE_MASK_FLAG_DDEWAIT = SEE_MASK_NOASYNC, 
        SEE_MASK_DOENVSUBST = 0x00000200,   
        SEE_MASK_FLAG_NO_UI = 0x00000400,   
        SEE_MASK_UNICODE = 0x00004000,
        SEE_MASK_NO_CONSOLE = 0x00008000,
        SEE_MASK_ASYNCOK = 0x00100000,
        SEE_MASK_HMONITOR = 0x00200000,   
        SEE_MASK_NOZONECHECKS = 0x00800000,
        SEE_MASK_NOQUERYCLASSSTORE = 0x01000000,
        SEE_MASK_WAITFORINPUTIDLE = 0x02000000,
        SEE_MASK_FLAG_LOG_USAGE = 0x04000000,
    }
```

## Tips & Tricks:
```cs
using System.Runtime.InteropServices;
```

## Tips & Tricks:
```cs
Imports System.Runtime.InteropServices
```

## Sample Code:
```cs
Dim info As SHELLEXECUTEINFO
info.cbSize = System.Runtime.InteropServices.Marshal.SizeOf(info)
info.lpVerb = "open"
info.lpFile = "somefile.html"
info.nShow = SW_SHOW
If Not ShellExecuteEx(info) Then
     Dim ex As New System.ComponentModel.Win32Exception(System.Runtime.InteropServices.Marshal.GetLastWin32Error())
     MessageBox.Show(ex.Message, "Error")
End If
```

## Alternative Managed API:
```cs
Dim p As New Process
p.StartInfo.FileName = "somefile.html"
p.StartInfo.ErrorDialog = True ' this opens the "Open With" dialog for unknown file types
p.Start()
```

## C# Example of Property Dialog
```cs
private const int SW_SHOW = 5;
private const uint SEE_MASK_INVOKEIDLIST = 12;

[DllImport("shell32.dll")]
static extern bool ShellExecuteEx(ref SHELLEXECUTEINFO lpExecInfo);

public static void ShowFileProperties(string Filename) {
    SHELLEXECUTEINFO info = new SHELLEXECUTEINFO();
    info.cbSize = System.Runtime.InteropServices.Marshal.SizeOf(info);
    info.lpVerb = "properties";
    info.lpFile = Filename;
    info.nShow = SW_SHOW;
    info.fMask = SEE_MASK_INVOKEIDLIST;
    ShellExecuteEx(ref info);
}
```

## VB.NET Example of Property Dialog
```cs
Public Const SW_SHOW As Short = 5
Public Const SEE_MASK_INVOKEIDLIST As Short = 12

<DllImport("Shell32", CharSet:=CharSet.Auto, SetLastError:=True)> _
    Public Shared Function ShellExecuteEx(ByRef lpExecInfo As SHELLEXECUTEINFO) As Boolean
    End Function

Dim sei As New SHELLEXECUTEINFO
sei.cbSize = Marshal.SizeOf(sei)
sei.lpVerb = "properties"
sei.lpFile = "FilePath"
sei.nShow = SW_SHOW
sei.fMask = SEE_MASK_INVOKEIDLIST
If Not ShellExecuteEx(sei) Then
   Dim ex As New System.ComponentModel.Win32Exception(System.Runtime.InteropServices.Marshal.GetLastWin32Error())
       MessageBox.Show(ex.Message, Me.TITLE, MessageBoxButtons.OK, MessageBoxIcon.Exclamation)
End If
```

## VB.NET Example of Property Dialog
```cs
"open"        - Opens a file or a application
"openas"    - Opens dialog when no program is associated to the extension
"opennew"    - see MSDN 
"runas"    - In Windows 7 and Vista, opens the UAC dialog and in others, open the Run as... Dialog
"null"     - Specifies that the operation is the default for the selected file type.
"edit"        - Opens the default text editor for the file.    
"explore"    - Opens the Windows Explorer in the folder specified in lpDirectory.
"properties"    - Opens the properties window of the file.
"copy"        - see MSDN
"cut"        - see MSDN
"paste"    - see MSDN
"pastelink"    - pastes a shortcut
"delete"    - see MSDN
"print"    - Start printing the file with the default application.
"printto"    - see MSDN
"find"        - Start a search
```
