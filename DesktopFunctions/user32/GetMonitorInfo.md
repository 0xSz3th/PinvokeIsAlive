
## C# Signature:
```cs
[DllImport("User32.dll")]
static extern bool GetMonitorInfo(IntPtr hMonitor, [In, Out] MONITORINFOEX lpmi);

[DllImport("user32.dll")]
static extern bool GetMonitorInfo(IntPtr hMonitor, [In, Out] MONITORINFO lpmi);
```

## Sample Code:
```cs
[DllImport("user32.dll")]
internal static extern bool EnumDisplayMonitors(IntPtr hdc, IntPtr lprcClip, MonitorEnumProc lpfnEnum, IntPtr dwData);

internal delegate bool MonitorEnumProc(IntPtr hMonitor, IntPtr hdcMonitor, ref RECT lprcMonitor, IntPtr dwData);

private void EnumMonitors()
{
    EnumDisplayMonitors(IntPtr.Zero, IntPtr.Zero, MonitorEnumCallBack, IntPtr.Zero);
}

private bool MonitorEnumCallBack(IntPtr hMonitor, IntPtr hdcMonitor, ref RECT lprcMonitor, IntPtr dwData)
{
    MONITORINFOEX mon_info = new MONITORINFOEX();
    mon_info.cbSize = (uint)Marshal.SizeOf(mon_info);
    GetMonitorInfo(hMonitor, ref mon_info);
    ///Monitor info is stored in 'mon_info'
    return true;
}
```
