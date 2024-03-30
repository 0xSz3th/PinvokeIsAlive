
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern uint GetGlyphOutline(IntPtr hdc, uint uChar, uint uFormat,
   out GLYPHMETRICS lpgm, uint cbBuffer, IntPtr lpvBuffer, ref MAT2 lpmat2);
```

## VB Signature
```cs
Public Declare Function GetGlyphOutline Lib "gdi32.dll"( _
   hdc As IntPtr, uChar As UInteger, uFormat As UInteger, _
   ByRef lpgm As GLYPHMETRICS, cbBuffer As UInteger, lpvBuffer As IntPtr, ByRef lpmat2 As MAT2) As Integer
```

## User-Defined Types:
```cs
public int cb;
    public int dwType;
    [MarshalAs(UnmanagedType.Struct)] public POINTFX pfxStart;
```

## User-Defined Types:
```cs
public struct TTPOLYCURVEHEADER
```

## User-Defined Types:
```cs
public short wType;
    public short cpfx;
```

## User-Defined Types:
```cs
public short fract;
    public short value;
```

## User-Defined Types:
```cs
[MarshalAs(UnmanagedType.Struct)] public FIXED eM11;
    [MarshalAs(UnmanagedType.Struct)] public FIXED eM12;
    [MarshalAs(UnmanagedType.Struct)] public FIXED eM21;
    [MarshalAs(UnmanagedType.Struct)] public FIXED eM22;
```

## User-Defined Types:
```cs
public struct POINT
```

## User-Defined Types:
```cs
public int x;
    public int y;
```

## User-Defined Types:
```cs
public struct POINTFX
```

## User-Defined Types:
```cs
[MarshalAs(UnmanagedType.Struct)] public FIXED x;
    [MarshalAs(UnmanagedType.Struct)] public FIXED y;
```

## User-Defined Types:
```cs
public struct GLYPHMETRICS
```

## User-Defined Types:
```cs
public int gmBlackBoxX;
    public int gmBlackBoxY;
    [MarshalAs(UnmanagedType.Struct)] public POINT gmptGlyphOrigin;
    public short gmCellIncX;
    public short gmCellIncY;
```

## Sample Code:
```cs
// Parse a glyph outline in native format
        public static void GetGlyphShape(Font font, Char c)
        {            
            GLYPHMETRICS metrics = new GLYPHMETRICS();            
            MAT2 matrix = new MAT2();
            matrix.eM11.value = 1;
            matrix.eM12.value = 0;
            matrix.eM21.value = 0;
            matrix.eM22.value = 1;

            using(Bitmap b = new Bitmap(1,1))
            {
                using(Graphics g = Graphics.FromImage(b))
                {
                    IntPtr hdc = g.GetHdc();                                        
                    IntPtr prev = SelectObject(hdc, font.ToHfont());                    
                    int bufferSize = (int)GetGlyphOutline(hdc, (uint)c, (uint)2, out metrics, 0, IntPtr.Zero, ref matrix);
                    IntPtr buffer = Marshal.AllocHGlobal(bufferSize);
                    try
                    {            
                        uint ret;
                        if((ret = GetGlyphOutline(hdc, (uint)c, (uint)2, out metrics, (uint)bufferSize, buffer, ref matrix)) > 0)
                        {                            
                            int polygonHeaderSize = Marshal.SizeOf(typeof(TTPOLYGONHEADER));
                            int curveHeaderSize = Marshal.SizeOf(typeof(TTPOLYCURVEHEADER));
                            int pointFxSize = Marshal.SizeOf(typeof(POINTFX));

                            int index = 0;
                            while(index < bufferSize)
                            {                                
                                TTPOLYGONHEADER header = (TTPOLYGONHEADER)Marshal.PtrToStructure(new IntPtr(buffer.ToInt32()+index), typeof(TTPOLYGONHEADER));

                                int startX = header.pfxStart.x.value;
                                int startY = -header.pfxStart.y.value;

                                // ...do something with start coords...
                                        int endCurvesIndex = index+header.cb;
                                index+=polygonHeaderSize;

                                while(index < endCurvesIndex)
                                {
                                    TTPOLYCURVEHEADER curveHeader = (TTPOLYCURVEHEADER)Marshal.PtrToStructure(new IntPtr(buffer.ToInt32()+index), typeof(TTPOLYCURVEHEADER));
                                    index+=curveHeaderSize;

                                    POINTFX[] curvePoints = new POINTFX[curveHeader.cpfx];

                                    for(int i = 0; i < curveHeader.cpfx; i++)
                                    {
                                        curvePoints[i] = (POINTFX)Marshal.PtrToStructure(new IntPtr(buffer.ToInt32()+index), typeof(POINTFX));
                                        index+=pointFxSize;
                                    }

                                    if(curveHeader.wType == (int)1)
                                    {
                                        // POLYLINE
                                        for(int i=0; i < curveHeader.cpfx; i++)
                                        {
                                            short x = curvePoints[i].x.value;
                                            short y = (short)-curvePoints[i].y.value;

    // ...do something with line points...

                                                                                }
                                    }
                                    else
                                    {
                                        // CURVE
                                        for(int i=0; i < curveHeader.cpfx - 1; i++)
                                        {
                                            POINTFX pfxB = curvePoints[i];
                                            POINTFX pfxC = curvePoints[i+1];

                                            short cx = pfxB.x.value;
                                            short cy = (short)-pfxB.y.value;

                                            short ax;
                                            short ay;

                                            if(i < curveHeader.cpfx - 2)
                                            {
                                                ax = (short)((pfxB.x.value+pfxC.x.value) / 2);
                                                ay = (short)-((pfxB.y.value+pfxC.y.value) / 2);
                                            }
                                            else
                                            {
                                                ax = pfxC.x.value;
                                                ay = (short)-pfxC.y.value;
                                            } // ...do something with curve points...
```

## Sample Code:
```cs
}
                                    }
                                }                                
                            }
                        }
                        else
                        {
                            throw new Exception("Could not retrieve glyph (GDI Error: 0x"+ret.ToString("X")+")");
                        }

                        g.ReleaseHdc(hdc);
                    }
                    finally
                    {                        
                        Marshal.FreeHGlobal(buffer);                    
                    }

                }
            }
            return shape;
        }
```
