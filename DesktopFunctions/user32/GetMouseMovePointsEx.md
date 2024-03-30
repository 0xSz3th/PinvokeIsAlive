
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern int GetMouseMovePointsEx(uint cbSize, [In] ref MOUSEMOVEPOINT
   lppt, [Out] MOUSEMOVEPOINT [] lpptBuf, int nBufPoints, uint resolution);
```

## Sample Code:
```cs
public const int GMMP_USE_DISPLAY_POINTS     = 1;
    public const int GMMP_USE_HIGH_RESOLUTION_POINTS = 2;

    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)] // For GetMouseMovePointsEx
    public struct MOUSEMOVEPOINT {
        public int x ;            //Specifies the x-coordinate of the mouse
        public int y ;            //Specifies the y-coordinate of the mouse
        public int time ;             //Specifies the time stamp of the mouse coordinate
        public IntPtr dwExtraInfo;        //Specifies extra information associated with this coordinate. 
    }

    [DllImport("user32.dll", ExactSpelling = true, CharSet = CharSet.Auto, SetLastError = true)]
    internal static extern int GetMouseMovePointsEx(
                    uint  cbSize,
                    [In] ref MOUSEMOVEPOINT pointsIn,
                    [Out] MOUSEMOVEPOINT[] pointsBufferOut,
                    int nBufPoints,
                    uint resolution
                   );

    uint mode  = GMMP_USE_DISPLAY_POINTS;

    MOUSEMOVEPOINT mp_in  = new MOUSEMOVEPOINT();
    MOUSEMOVEPOINT[] mp_out = new MOUSEMOVEPOINT[64];
    int nNumPointsRequired = 20 ; // set number of points to desired value less than 64

    // Set the Current Position in currentPosition, of type POINT

    mp_in.x = ((int)currentPosition.X) & 0x0000FFFF;  //Ensure that this number will pass through.
    mp_in.y = ((int)currentPosition.Y) & 0x0000FFFF;

    int cpt = GetMouseMovePointsEx((uint)(Marshal.SizeOf(mp_in)), ref mp_in, mp_out, nNumPointsRequired, mode);
    if (cpt == -1)
    {
       int win32Error = Marshal.GetLastWin32Error(); // Dance around FxCop.
        throw new System.ComponentModel.Win32Exception(win32Error);
    }
```
