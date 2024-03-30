
## C# Signature:
```cs
[DllImport("gdi32.dll", EntryPoint="GetCharacterPlacementW")]
    static extern uint GetCharacterPlacementW(IntPtr hdc, [MarshalAs(UnmanagedType.LPWStr)] string lpString,
       int nCount, int nMaxExtent, ref GCP_RESULTS lpResults, uint dwFlags);
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct GCP_RESULTS
    {
        public int StructSize;
        [MarshalAs(UnmanagedType.LPTStr)]
        public string OutString;
        public IntPtr Order;
        public IntPtr Dx;
        public IntPtr CaretPos;
        public IntPtr Class;
        public IntPtr Glyphs;
        public int GlyphCount;
        public int MaxFit;
    }

    [Flags]
    public enum GCPFlags : uint
    {
        GCP_DBCS = 0x0001,
        GCP_REORDER = 0x0002,
        GCP_USEKERNING = 0x0008,
        GCP_GLYPHSHAPE = 0x0010,
        GCP_LIGATE = 0x0020,
        GCP_DIACRITIC = 0x0100,
        GCP_KASHIDA = 0x0400,
        GCP_ERROR = 0x8000,
        GCP_JUSTIFY = 0x00010000,
        GCP_CLASSIN = 0x00080000,
        GCP_MAXEXTENT = 0x00100000,
        GCP_JUSTIFYIN = 0x00200000,
        GCP_DISPLAYZWG = 0x00400000,
        GCP_SYMSWAPOFF = 0x00800000,
        GCP_NUMERICOVERRIDE = 0x01000000,
        GCP_NEUTRALOVERRIDE = 0x02000000,
        GCP_NUMERICSLATIN = 0x04000000,
        GCP_NUMERICSLOCAL = 0x08000000,
    }
```

## Sample Code:
```cs
public int GetCaretPostion(string str, int index)
    {
        IntPtr OldFont = SelectObject(this.DC, this.Font);

        int len = str.Length;
        int[] order = new int[len];
        int[] dx = new int[len];
        int[] caret = new int[len];
        byte[] clss = new byte[len];
        short[] glys = new short[len];

        GCHandle ordHnd = GCHandle.Alloc(order, GCHandleType.Pinned);
        GCHandle dxHnd = GCHandle.Alloc(dx, GCHandleType.Pinned);
        GCHandle carHnd = GCHandle.Alloc(caret, GCHandleType.Pinned);
        GCHandle clsHnd = GCHandle.Alloc(clss, GCHandleType.Pinned);
        GCHandle glyHnd = GCHandle.Alloc(glys, GCHandleType.Pinned);

        try
        {
        GCP_RESULTS rs = new GCP_RESULTS();
        rs.StructSize = Marshal.SizeOf(typeof(GCP_RESULTS));

        rs.OutString = new String('\0', len + 2);
        rs.Order = ordHnd.AddrOfPinnedObject();
        rs.Dx = dxHnd.AddrOfPinnedObject();
        rs.CaretPos = carHnd.AddrOfPinnedObject();
        rs.Class = clsHnd.AddrOfPinnedObject();
        rs.Glyphs = glyHnd.AddrOfPinnedObject();

        rs.GlyphCount = len;
        rs.MaxFit = 0;

        GCPFlags flg = GCPFlags.GCP_GLYPHSHAPE;
        uint r = GetCharacterPlacement(this.DC, str, len, 0, ref rs, (uint)flg);
        if (r == 0)
            throw new Exception(string.Format("GeCharacterPlacement Error {0}", Marshal.GetLastWin32Error()));
        }
        finally
        {
        ordHnd.Free();
        dxHnd.Free();
        carHnd.Free();
        clsHnd.Free();
        glyHnd.Free();
        } 

        SelectObject(this.DC, OldFont);

        return caret[index];
    }
```
