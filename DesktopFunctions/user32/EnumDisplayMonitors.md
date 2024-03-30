
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool EnumDisplayMonitors(IntPtr hdc, IntPtr lprcClip,
   EnumMonitorsDelegate lpfnEnum, IntPtr dwData);

[StructLayout(LayoutKind.Sequential)]
public struct Rect
{
    public int left;
    public int top;
    public int right;
    public int bottom;
}

delegate bool EnumMonitorsDelegate(IntPtr hMonitor, IntPtr hdcMonitor, ref Rect lprcMonitor, IntPtr dwData);
```

## Vb.Net Signature:
```cs
<DllImport("user32.dll")> _
Private Shared Function EnumDisplayMonitors(ByVal hdc As IntPtr, ByVal lprcClip As IntPtr, ByVal lpfnEnum As EnumMonitorsDelegate, ByVal dwData As IntPtr) As Boolean
End Function

<StructLayout(LayoutKind.Sequential)> _
Public Structure Rect
    Private Left As Integer, Top As Integer, Right As Integer, Bottom As Integer
End Structure

Delegate Function EnumMonitorsDelegate(hMonitor As IntPtr, hdcMonitor As IntPtr, ByRef lprcMonitor As Rect, dwData As IntPtr) As Boolean
```

## Sample Code:
```cs
/// <summary>
    /// The struct that contains the display information
    /// </summary>
    public class DisplayInfo
    {
        public string Availability { get; set; }
        public string ScreenHeight { get; set; }
        public string ScreenWidth { get; set; }
        public Rect MonitorArea { get; set; }
        public Rect WorkArea { get; set; }
    }

    /// <summary>
    /// Collection of display information
    /// </summary>
    public class DisplayInfoCollection : List<DisplayInfo>
    {
    }

    /// <summary>
    /// Returns the number of Displays using the Win32 functions
    /// </summary>
    /// <returns>collection of Display Info</returns>
    public DisplayInfoCollection GetDisplays()
    {
    DisplayInfoCollection col = new DisplayInfoCollection();

    EnumDisplayMonitors( IntPtr.Zero, IntPtr.Zero, 
        delegate (IntPtr hMonitor, IntPtr hdcMonitor, ref Rect lprcMonitor,  IntPtr dwData)
        {
        MonitorInfo mi = new MonitorInfo();
        mi.size = (uint)Marshal.SizeOf(mi);
        bool success = GetMonitorInfo(hMonitor, ref mi);
        if (success)
        {
            DisplayInfo di = new DisplayInfo();
            di.ScreenWidth = (mi.monitor.right - mi.monitor.left).ToString();
            di.ScreenHeight = (mi.monitor.bottom - mi.monitor.top).ToString();
            di.MonitorArea = mi.monitor;
            di.WorkArea = mi.work;
            di.Availability = mi.flags.ToString();
            col.Add(di);
        }
        return true;
         }, IntPtr.Zero );
     return col;
    }
```
