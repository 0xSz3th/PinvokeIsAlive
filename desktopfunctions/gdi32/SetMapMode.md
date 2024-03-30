
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern int SetMapMode(IntPtr hdc, int fnMapMode);
```

## Constants:
```cs
//Mapping Modes
static int MM_TEXT = 1;
static int MM_LOMETRIC = 2;
static int MM_HIMETRIC = 3;
static int MM_LOENGLISH = 4;
static int MM_HIENGLISH = 5;
static int MM_TWIPS = 6;
static int MM_ISOTROPIC = 7;
static int MM_ANISOTROPIC = 8;

//Minimum and Maximum Mapping Mode values
static int MM_MIN = MM_TEXT;
static int MM_MAX = MM_ANISOTROPIC;
static int MM_MAX_FIXEDSCALE = MM_TWIPS;
```

## Sample Code:
```cs
[DllImport("gdi32.dll")] 
    static extern int SetMapMode(IntPtr hDC, int nMapMode);

    [DllImport("gdi32.dll")]
    static extern bool SetViewportOrgEx(IntPtr hDC, int x, int y, Point[] prevPoint);

    [DllImport("gdi32.dll")]
    static extern bool SetWindowOrgEx(IntPtr hDC, int x, int y, Point[] prevPoint);

    [DllImport("gdi32.dll")]
    static extern bool SetViewportExtEx(IntPtr hDC, int nExtentX, int nExtentY, Size[] prevSize);

    [DllImport("gdi32.dll")]
    static extern bool SetWindowExtEx(IntPtr hDC, int nExtentX, int nExtentY, Size[] prevSize);

    [DllImport("Gdi32.dll")]
    public static extern int CreatePen(int nPenStyle, int nWidth, int nColor);

    [DllImport("Gdi32.dll")]
    public static extern int GetStockObject(int nStockBrush);

    [DllImport("Gdi32.dll")]
    public static extern int SelectObject(IntPtr hDC, int hGdiObject);

    [DllImport("Gdi32.dll")]
    public static extern int DeleteObject(int hBitmap);

    [DllImport("Gdi32.dll")]
    public static extern int MoveToEx(IntPtr hDC, int x, int y, int nPreviousPoint);

    [DllImport("Gdi32.dll")]
    public static extern int LineTo(IntPtr hDC, int x, int y);

    [DllImport("Gdi32.dll")]
    public static extern int Rectangle(IntPtr hDC, int nLeft, int nTop, int nRight, int nBottom);

    [DllImport("Gdi32.dll")]
    public static extern bool DPtoLP(IntPtr hdc, [In, Out] Point[] lpPoints, int nCount);

    // Mapping modes.
    const int MM_TEXT = 1; 
    const int MM_LOMETRIC = 2; 
    const int MM_HIMETRIC = 3; 
    const int MM_LOENGLISH = 4;
    const int MM_HIENGLISH = 5;
    const int MM_TWIPS = 6;
    const int MM_ISOTROPIC = 7;
    const int MM_ANISOTROPIC = 8;

    // Gdi stock objects.
    const int WHITE_BRUSH = 0;
    const int LTGRAY_BRUSH = 1;
    const int GRAY_BRUSH = 2;
    const int DKGRAY_BRUSH = 3;
    const int BLACK_BRUSH = 4;
    const int NULL_BRUSH = 5;
    const int HOLLOW_BRUSH = NULL_BRUSH;
    const int WHITE_PEN = 6;
    const int BLACK_PEN = 7;
    const int NULL_PEN = 8;
    const int OEM_FIXED_FONT = 10;
    const int ANSI_FIXED_FONT = 11;
    const int ANSI_VAR_FONT = 12;
    const int SYSTEM_FONT = 13;
    const int DEVICE_DEFAULT_FONT = 14;
    const int DEFAULT_PALETTE = 15;
    const int SYSTEM_FIXED_FONT = 16;

    // Pen styles.
    const int PS_SOLID = 0;
    const int PS_DASH = 1;
    const int PS_DOT = 2;
    const int PS_DASHDOT = 3;
    const int PS_DASHDOTDOT = 4;
    const int PS_NULL = 5;
    const int PS_INSIDEFRAME = 6;
    const int PS_USERSTYLE = 7;
    const int PS_ALTERNATE = 8;
    const int PS_STYLE_MASK = 0x0000000F;
    const int PS_ENDCAP_ROUND = 0x00000000;
    const int PS_ENDCAP_SQUARE = 0x00000100;
    const int PS_ENDCAP_FLAT = 0x00000200;
    const int PS_ENDCAP_MASK = 0x00000F00;
    const int PS_JOIN_ROUND = 0x00000000;
    const int PS_JOIN_BEVEL = 0x00001000;
    const int PS_JOIN_MITER = 0x00002000;
    const int PS_JOIN_MASK = 0x0000F000;
    const int PS_COSMETIC = 0x00000000;
    const int PS_GEOMETRIC = 0x00010000;
    const int PS_TYPE_MASK = 0x000F0000;

     ...
     ...
     ...
```

## Sample Code:
```cs
hDC,
         0,
         this.ClientRectangle.Bottom,    // So that (0,0) is at the bottom left.
         point);
```

## Sample Code:
```cs
hDC,
           0,
           0,
           point);
```

## Sample Code:
```cs
hDC,
         this.ClientRectangle.Right,
         -this.ClientRectangle.Bottom, // Negative so that y gets positive as you go up.
         size);
```

## Sample Code:
```cs
hDC,
       1000,
           (int)(1000 * fAspectRatio),
           size);
```
