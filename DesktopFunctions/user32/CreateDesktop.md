
## C# Signature:
```cs
// ms-help://MS.VSCC.v80/MS.MSDN.v80/MS.WIN32COM.v10.en/dllproc/base/createdesktop.htm
    [DllImport("user32.dll", EntryPoint="CreateDesktop", CharSet=CharSet.Unicode, SetLastError=true)]
    public static extern IntPtr CreateDesktop(
                    [MarshalAs(UnmanagedType.LPWStr)] string desktopName,
                    [MarshalAs(UnmanagedType.LPWStr)] string device, // must be null.
                    [MarshalAs(UnmanagedType.LPWStr)] string deviceMode, // must be null,
                    [MarshalAs(UnmanagedType.U4)] int flags,  // use 0
                    [MarshalAs(UnmanagedType.U4)] ACCESS_MASK accessMask,
                    [MarshalAs(UnmanagedType.LPStruct)] SECURITY_ATTRIBUTES attributes);


    // ms-help://MS.VSCC.v80/MS.MSDN.v80/MS.WIN32COM.v10.en/dllproc/base/closedesktop.htm
    [DllImport("user32.dll", EntryPoint="CloseDesktop", CharSet =  CharSet.Unicode, SetLastError = true)]
    [return: MarshalAs(UnmanagedType.Bool)]
    public static extern bool CloseDesktop(IntPtr handle);
```

## VB.NET Signature:
```cs
' ms-help://MS.VSCC.v80/MS.MSDN.v80/MS.WIN32COM.v10.en/dllproc/base/createdesktop.htm
    <DllImport("user32.dll", EntryPoint:="CreateDesktop", CharSet:=CharSet.Unicode, SetLastError:=True)> _
    Public Shared Function CreateDesktop(ByVal desktopName As String, ByVal device As String, 
                           ByVal deviceMode As String, ByVal flags As Integer, 
                           ByVal accessMask As ACCESS_MASK, ByVal attributes As SECURITY_ATTRIBUTES) As IntPtr
    End Function

    ' ms-help://MS.VSCC.v80/MS.MSDN.v80/MS.WIN32COM.v10.en/dllproc/base/closedesktop.htm
    <DllImport("user32.dll", EntryPoint:="CloseDesktop", CharSet:=CharSet.Unicode, SetLastError:=True)> _
    Public Shared Function CloseDesktop(ByVal handle As IntPtr) As <MarshalAs(UnmanagedType.Bool)> Boolean
    End Function
```

## Notes:
```cs
static extern IntPtr CreateDesktop(..., [In] ref SECURITY_ATTRIBUTES lpsa);
```

## Notes:
```cs
[MarshalAs(UnmanagedType.LPStruct)] SECURITY_ATTRIBUTES attributes);
```

## Sample Code:
```cs
public class SafeDesktopHandle : BaseSafeHandle
    {
    public SafeDesktopHandle(IntPtr handle, bool ownsHandle)
        : base(handle, ownsHandle)
    { }

    protected override bool CloseNativeHandle(IntPtr handle)
    {
        return WindowStationAndDesktop.CloseDesktop(handle);
    }
    }
[Flags]
    internal enum ACCESS_MASK : uint
    {
    DESKTOP_NONE        = 0,
    DESKTOP_READOBJECTS     = 0x0001,
    DESKTOP_CREATEWINDOW    = 0x0002,
    DESKTOP_CREATEMENU      = 0x0004,
    DESKTOP_HOOKCONTROL     = 0x0008,
    DESKTOP_JOURNALRECORD       = 0x0010,
    DESKTOP_JOURNALPLAYBACK     = 0x0020,
    DESKTOP_ENUMERATE       = 0x0040,
    DESKTOP_WRITEOBJECTS    = 0x0080,
    DESKTOP_SWITCHDESKTOP       = 0x0100,

    GENERIC_ALL         = ( DESKTOP_READOBJECTS | DESKTOP_CREATEWINDOW | DESKTOP_CREATEMENU |
                    DESKTOP_HOOKCONTROL | DESKTOP_JOURNALRECORD | DESKTOP_JOURNALPLAYBACK |
                    DESKTOP_ENUMERATE | DESKTOP_WRITEOBJECTS | DESKTOP_SWITCHDESKTOP |
                    STANDARD_ACCESS.STANDARD_RIGHTS_REQUIRED),
    }
```
