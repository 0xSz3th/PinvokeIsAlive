
## C# Signature:
```cs
[DllImport("shell32.dll")]
static extern bool Shell_NotifyIcon(uint dwMessage,
   [In] ref NOTIFYICONDATA pnid);
```

## VB.NET Signature
```cs
<DllImport("shell32.dll")> _
Shared Function Shell_NotifyIcon(dwMessage as UInteger, ByRef pnid as NOTIFYICONDATA) as Boolean
End Function
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct NotifyIconData
    {
        public System.Int32 cbSize; // DWORD
        public System.IntPtr hWnd; // HWND
        public System.Int32 uID; // UINT
        public NotifyFlags uFlags; // UINT
        public System.Int32 uCallbackMessage; // UINT
        public System.IntPtr hIcon; // HICON
        [MarshalAs(UnmanagedType.ByValTStr, SizeConst=128)]
        public System.String szTip; // char[128]
        public System.Int32 dwState; // DWORD
        public System.Int32 dwStateMask; // DWORD
        [MarshalAs(UnmanagedType.ByValTStr, SizeConst=256)]
        public System.String szInfo; // char[256]
        public System.Int32 uTimeoutOrVersion; // UINT
        [MarshalAs(UnmanagedType.ByValTStr, SizeConst=64)]
        public System.String szInfoTitle; // char[64]
        public System.Int32 dwInfoFlags; // DWORD
        //GUID guidItem; > IE 6
    }
```

## User-Defined Types:
```cs
public enum NotifyIconMessage : int
    {
        NIM_ADD      = 0x00000000,
        NIM_MODIFY       = 0x00000001,
        NIM_DELETE       = 0x00000002,
        NIM_SETFOCUS     = 0x00000003,
        NIM_SETVERSION   = 0x00000004,
    }
```
