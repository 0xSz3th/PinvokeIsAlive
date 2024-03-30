
## C# Signature:
```cs
[DllImport("winmm.dll")]
static extern Int32 mixerSetControlDetails(IntPtr hmxobj,
   ref MixerControlDetails pmxcd, UInt32 fdwDetails);
```

## VB Signature:
```cs
Declare Function mixerSetControlDetails Lib "winmm.dll" (ByVal hmxobj As IntPtr, ByVal pmxcd As MIXERCONTROLDETAILS, ByVal fdwDetails As Integer) As Integer
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi, Pack = 4)]
public struct MIXERCONTROL
{
     private UInt32 cbStruct;
     private UInt32 dwControlID;
     private UInt32 dwControlType;
     private UInt32 fdwControl;
     private UInt32 cMultipleItems;
     [MarshalAs(UnmanagedType.ByValTStr, SizeConst = MixerXPNative.MIXER_SHORT_NAME_CHARS)]
     private string szShortName;
     [MarshalAs(UnmanagedType.ByValTStr, SizeConst = MixerXPNative.MIXER_LONG_NAME_CHARS)]
     private string szName;
     public MIXERCONTROL_BOUNDS Bounds;
     public MIXERCONTROL_METRICS Metrics;

     #region Properties

     /// <summary>size in bytes of <see cref="MIXERCONTROL">MIXERCONTROL</see></summary>
     public UInt32 StructSize
     {
        get { return this.cbStruct; }
        set { this.cbStruct = value; }
     }
     /// <summary></summary>
     public UInt32 ControlID
     {
        get { return this.dwControlID; }
        set { this.dwControlID = value; }
     }
     /// <summary>MIXERCONTROL_CONTROLTYPE_xxx</summary>
     public MIXERCONTROL_CONTROLTYPE ControlType
     {
        get { return (MIXERCONTROL_CONTROLTYPE)this.dwControlType; }
        set { this.dwControlType = (UInt32)value; }
     }
     /// <summary>MIXERCONTROL_CONTROLF_xxx</summary>
     public MIXERCONTROL_CONTROLF Control
     {
        get { return (MIXERCONTROL_CONTROLF)this.fdwControl; }
        set { this.fdwControl = (uint)value; }
     }
     /// <summary>if MIXERCONTROL_CONTROLF_MULTIPLE set</summary>
     public UInt32 MultipleItems
     {
        get { return this.cMultipleItems; }
        set { this.cMultipleItems = value; }
     }
     /// <summary></summary>
     public String ShortName
     {
        get { return this.szShortName; }
        set { this.szShortName = value; }
     }
     /// <summary></summary>
     public String Name
     {
        get { return this.szName; }
        set { this.szName = value; }
     }

     #endregion
}

[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi, Pack = 4)]
public struct MIXERCONTROL_BOUNDS
{
     private Int32 lMinimum;
     private Int32 lMaximum;
     //public uint dwMinimum; // Unioned with lMinimum
     //public uint dwMaximum; // Unioned with lMaximum
     //public uint dwReserved1; // Unioned with lMinimum
     //public uint dwReserved2; // Unioned with lMaximum
     private UInt32 dwReserved3;
     private UInt32 dwReserved4;
     private UInt32 dwReserved5;
     private UInt32 dwReserved6;

     #region Properties

     /// <summary>signed minimum for this control</summary>
     public Int32 Minimum
     {
        get { return this.lMinimum; }
        set { this.lMinimum = value; }
     }
     /// <summary>signed maximum for this control</summary>
     public Int32 Maximum
     {
        get { return this.lMaximum; }
        set { this.lMaximum = value; }
     }
     /// <summary>unsigned minimum for this control</summary>
     public UInt32 UnsignedMinimum
     {
        get { return (uint)this.lMinimum; }//TODO: something different
        set { this.lMinimum = (int)value; }
     }
     /// <summary>unsigned maximum for this control</summary>
     public UInt32 UnsignedMaximum
     {
        get { return (uint)this.lMaximum; }//TODO: something different
        set { this.lMaximum = (int)value; }
     }
     /// <summary></summary>
     public UInt32 Reserved1
     {
        get { return (uint)this.lMinimum; }//TODO: something different
        set { this.lMinimum = (int)value; }
     }
     /// <summary></summary>
     public UInt32 Reserved2
     {
        get { return (uint)this.lMaximum; }//TODO: something different
        set { this.lMaximum = (int)value; }
     }
     /// <summary></summary>
     public UInt32 Reserved3
     {
        get { return this.dwReserved3; }
        set { this.dwReserved3 = value; }
     }
     /// <summary></summary>
     public UInt32 Reserved4
     {
        get { return this.dwReserved4; }
        set { this.dwReserved4 = value; }
     }
     /// <summary></summary>
     public UInt32 Reserved5
     {
        get { return this.dwReserved5; }
        set { this.dwReserved5 = value; }
     }
     /// <summary></summary>
     public UInt32 Reserved6
     {
        get { return this.dwReserved6; }
        set { this.dwReserved6 = value; }
     }

     #endregion
}

[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi, Pack = 4)]
public struct MIXERCONTROL_METRICS
{
     private UInt32 cSteps;
     //private UInt32 cbCustomData; //Unioned with cSteps
     //private UInt32 dwReserved1; //Unioned with cSteps
     private UInt32 dwReserved2;
     private UInt32 dwReserved3;
     private UInt32 dwReserved4;
     private UInt32 dwReserved5;
     private UInt32 dwReserved6;

     #region Properties

     /// <summary># of steps between min & max</summary>
     public UInt32 Steps
     {
        get { return this.cSteps; }
        set { this.cSteps = value; }
     }
     /// <summary>size in bytes of custom data</summary>
     public UInt32 CustomData
     {
        get { return this.cSteps; }
        set { this.cSteps = value; }
     }
     /// <summary>!!! needed? we have cbStruct....</summary>
     public UInt32 Reserved1
     {
        get { return this.cSteps; }//TODO: something different
        set { this.cSteps = value; }
     }
     /// <summary>!!! needed? we have cbStruct....</summary>
     public UInt32 Reserved2
     {
        get { return this.dwReserved2; }
        set { this.dwReserved2 = value; }
     }
     /// <summary>!!! needed? we have cbStruct....</summary>
     public UInt32 Reserved3
     {
        get { return this.dwReserved3; }
        set { this.dwReserved3 = value; }
     }
     /// <summary>!!! needed? we have cbStruct....</summary>
     public UInt32 Reserved4
     {
        get { return this.dwReserved4; }
        set { this.dwReserved4 = value; }
     }
     /// <summary>!!! needed? we have cbStruct....</summary>
     public UInt32 Reserved5
     {
        get { return this.dwReserved5; }
        set { this.dwReserved5 = value; }
     }
     /// <summary>!!! needed? we have cbStruct....</summary>
     public UInt32 Reserved6
     {
        get { return this.dwReserved6; }
        set { this.dwReserved6 = value; }
     }

     #endregion
}
```

## User-Defined Types:
```cs
Structure MIXERCONTROLDETAILS
     Dim cbStruct As Integer
     Dim dwControlID As Integer
     Dim cChannels As Integer
     Structure u ' A union
     Dim hWndOwner As IntPtr
     Dim cMultipleItems As Integer
     End Structure
     Dim cbDetails As Integer
     Dim paDeatails As IntPtr
End Structure
```

## Tips & Tricks:
```cs
[DllImport("winmm.dll", CharSet = CharSet.Unicode)]
private static extern Int32 mixerSetControlDetails(IntPtr hmxobj, ref MIXERCONTROLDETAILS pmxcd, uint fdwDetails);

public static Int32 mixerSetControlDetails(IntPtr hmxobj, ref MIXERCONTROLDETAILS pmxcd, MIXER_OBJECTF fdwDetails, MIXER_SETCONTROLDETAILSF setControlDetails)
{
     uint flags = ((uint)fdwDetails | (uint)setControlDetails);
     return mixerSetControlDetails(hmxobj, ref pmxcd, flags);
}

public enum MIXER_OBJECTF : uint
{
     HANDLE   = 0x80000000u,
     MIXER    = 0x00000000u,
     HMIXER   = (HANDLE | MIXER),
     WAVEOUT  = 0x10000000u,
     HWAVEOUT = (HANDLE | WAVEOUT),
     WAVEIN   = 0x20000000u,
     HWAVEIN  = (HANDLE | WAVEIN),
     MIDIOUT  = 0x30000000u,
     HMIDIOUT = (HANDLE | MIDIOUT),
     MIDIIN   = 0x40000000u,
     HMIDIIN  = (HANDLE | MIDIIN),
     AUX      = 0x50000000u,
}
public enum MIXER_SETCONTROLDETAILSF : uint
{
     VALUE      = 0x00000000u,
     CUSTOM     = 0x00000001u,

     QUERYMASK  = 0x0000000Fu,
}
```
