IntPtr hWinPosInfo,
        IntPtr hWnd,           // window handle
        IntPtr hWndInsertAfter,    // placement-order handle
        int X,             // horizontal position
        int Y,             // vertical position
        int cx,            // width
        int cy,            // height
        uint uFlags);          // window positioning flags
public static IntPtr
    NoTopMost = new IntPtr(-2),
    TopMost = new IntPtr(-1),
    Top = new IntPtr(0),
    Bottom = new IntPtr(1);
public static readonly uint
    NOSIZE = 0x0001,
    NOMOVE = 0x0002,
    NOZORDER = 0x0004,
    NOREDRAW = 0x0008,
    NOACTIVATE = 0x0010,
    DRAWFRAME = 0x0020,
    FRAMECHANGED = 0x0020,
    SHOWWINDOW = 0x0040,
    HIDEWINDOW = 0x0080,
    NOCOPYBITS = 0x0100,
    NOOWNERZORDER = 0x0200,
    NOREPOSITION = 0x0200,
    NOSENDCHANGING = 0x0400,
    DEFERERASE = 0x2000,
    ASYNCWINDOWPOS = 0x4000;
