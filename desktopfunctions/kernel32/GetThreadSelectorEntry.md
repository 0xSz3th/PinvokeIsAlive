
## C# Signature:
```cs
[DllImport( "kernel32.dll", SetLastError = true )]
    static extern bool GetThreadSelectorEntry (
        IntPtr hThread,
        uint dwSelector,
        out LDT_ENTRY lpSelectorEntry
        );
```

## C# Signature:
```cs
struct BYTES
    {
        public byte BaseMid;
        public byte Flags1;
        public byte Flags2;
        public byte BaseHi;
    }

    struct BITS
    {
        int Value;
        /// <summary>
        /// Max set value is 255 (11111111b)
        /// </summary>
        public int BaseMid {
        get {
            return ( Value & 0xFF );
        }
        set {
            Value = ( Value & unchecked( (int)0xFFFFFF00 ) ) | ( value & 0xFF );
        }
        }
        /// <summary>
        /// Max set value is 31 (11111b)
        /// </summary>
        public int Type {
        get {
            return ( Value & 0x1F00 ) >> 8;
        }
        set {
            Value = ( Value & unchecked( (int)0xFFFFE0FF ) ) | ( ( value & 0x1F ) << 8 );
        }
        }
        /// <summary>
        /// Max set value is 3 (11b)
        /// </summary>
        public int Dpl {
        get {
            return ( Value & 0x6000 ) >> 13;
        }
        set {
            Value = ( Value & unchecked( (int)0xFFFF9FFF ) ) | ( ( value & 0x3 ) << 13 );
        }
        }
        /// <summary>
        /// Max set value is 1 (1b)
        /// </summary>
        public int Pres {
        get {
            return ( Value & 0x4000 ) >> 15;
        }
        set {
            Value = ( Value & unchecked( (int)0xFFFFBFFF ) ) | ( ( value & 0x1 ) << 15 );
        }
        }
        /// <summary>
        /// Max set value is 15 (1111b)
        /// </summary>
        public int LimitHi {
        get {
            return ( Value & 0xF0000 ) >> 16;
        }
        set {
            Value = ( Value & unchecked( (int)0xFFF0FFFF ) ) | ( ( value & 0xF ) << 16 );
        }
        }
        /// <summary>
        /// Max set value is 1 (1b)
        /// </summary>
        public int Sys {
        get {
            return ( Value & 0x100000 ) >> 20;
        }
        set {
            Value = ( Value & unchecked( (int)0xFFEFFFFF ) ) | ( ( value & 0x1 ) << 20 );
        }
        }
        /// <summary>
        /// Max set value is 1 (1b)
        /// </summary>
        public int Reserved_0 {
        get {
            return ( Value & 0x200000 ) >> 21;
        }
        set {
            Value = ( Value & unchecked( (int)0xFFDFFFFF ) ) | ( ( value & 0x1 ) << 21 );
        }
        }
        /// <summary>
        /// Max set value is 1 (1b)
        /// </summary>
        public int Default_Big {
        get {
            return ( Value & 0x400000 ) >> 22;
        }
        set {
            Value = ( Value & unchecked( (int)0xFFBFFFFF ) ) | ( ( value & 0x1 ) << 22 );
        }
        }
        /// <summary>
        /// Max set value is 1 (1b)
        /// </summary>
        public int Granularity {
        get {
            return ( Value & 0x800000 ) >> 23;
        }
        set {
            Value = ( Value & unchecked( (int)0xFF7FFFFF ) ) | ( ( value & 0x1 ) << 23 );
        }
        }
        /// <summary>
        /// Max set value is 255 (11111111b)
        /// </summary>
        public int BaseHi {
        get {
            return ( Value & unchecked( (int)0xFF000000 ) ) >> 24;
        }
        set {
            Value = ( Value & unchecked( (int)0xFFFFFF ) ) | ( ( value & 0xFF ) << 24 );
        }
        }
    }

    [StructLayout( LayoutKind.Explicit )]
    struct HIGHWORD
    {
        [FieldOffset( 0 )]
        public BYTES Bytes;
        [FieldOffset( 0 )]
        public BITS Bits;
    }

    struct LDT_ENTRY
    {
        public ushort LimitLow;
        public ushort BaseLow;
        public HIGHWORD HighWord;
    }
```

## C# Signature:
```cs
var cntx = new CONTEXT();
    LDT_ENTRY ldt;

    cntx.ContextFlags = CONTEXT_ALL;

    if ( !GetThreadContext( GetCurrentThread(), ref cntx ) )
        throw new Exception();

    if ( !GetThreadSelectorEntry( GetCurrentThread(), cntx.SegDs, out ldt ) )
        throw new Exception();
```
