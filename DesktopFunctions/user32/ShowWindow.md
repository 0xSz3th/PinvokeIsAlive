
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool ShowWindow(IntPtr hWnd, int nCmdShow);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Public Shared Function ShowWindow(hWnd As IntPtr, <MarshalAs(UnmanagedType.I4)>nCmdShow As ShowWindowCommands) As <MarshalAs(UnmanagedType.Bool)> Boolean
End Function
```

## VB Signature:
```cs
Public Declare Function ShowWindow Lib "user32" _
         (ByVal hWnd As Long, _
          ByVal nCmdShow As Long) As Long
```

## Sample Code:
```cs
[DllImport("user32.dll")]
private static extern bool ShowWindow(IntPtr hWnd, int nCmdShow);

private const int SW_RESTORE = 9;
IntPtr i= (Int64)this.Handle;
ShowWindowAsync(i, SW_RESTORE);
```

## Sample Code:
```cs
using System.Runtime.InteropServices;
using System.Diagnostics;

[DllImport("user32.dll")]
private static extern bool ShowWindow(IntPtr hWnd, int nCmdShow);

IntPtr handle = Process.GetCurrentProcess( ).MainWindowHandle;
ShowWindowAsync(handle, 0);
```
