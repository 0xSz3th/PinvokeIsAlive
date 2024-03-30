
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi, Pack = 4)]
public struct MIXERLINE
{
     private UInt32 cbStruct;
     private UInt32 dwDestination;
     private UInt32 dwSource;
     private UInt32 dwLineID;
     private UInt32 fdwLine;
     private IntPtr dwUser;
     private UInt32 dwComponentType;
     private UInt32 cChannels;
     private UInt32 cConnections;
     private UInt32 cControls;
     [MarshalAs(UnmanagedType.ByValTStr, SizeConst = MixerXPNative.MIXER_SHORT_NAME_CHARS)]
     private string szShortName;
     [MarshalAs(UnmanagedType.ByValTStr, SizeConst = MixerXPNative.MIXER_LONG_NAME_CHARS)]
     private string szName;
     public MIXERLINETARGET Target;

     #region Properties

     /// <summary>size of MIXERLINE structure</summary>
     public UInt32 StructSize
     {
        get { return this.cbStruct; }
        set { this.cbStruct = value; }
     }
     /// <summary>zero based destination index</summary>
     public UInt32 Destination
     {
        get { return this.dwDestination; }
        set { this.dwDestination = value; }
     }
     /// <summary>zero based source index (if source)</summary>
     public UInt32 Source
     {
        get { return this.dwSource; }
        set { this.dwSource = value; }
     }
     /// <summary>unique line id for mixer device</summary>
     public UInt32 LineID
     {
        get { return this.dwLineID; }
        set { this.dwLineID = value; }
     }
     /// <summary>state/information about line</summary>
     public MIXERLINE_LINEF LineInformation
     {
        get { return (MIXERLINE_LINEF)this.fdwLine; }
        set { this.fdwLine = (UInt32)value; }
     }
     /// <summary>driver specific information</summary>
     public IntPtr UserPointer
     {
        get { return this.dwUser; }
        set { this.dwUser = value; }
     }
     /// <summary>component type line connects to</summary>
     public MIXERLINE_COMPONENTTYPE ComponentType
     {
        get { return (MIXERLINE_COMPONENTTYPE)this.dwComponentType; }
        set { this.dwComponentType = (UInt32)value; }
     }
     /// <summary>number of channels line supports</summary>
     public UInt32 Channels
     {
        get { return this.cChannels; }
        set { this.cChannels = value; }
     }
     /// <summary>number of connections [possible]</summary>
     public UInt32 Connections
     {
        get { return this.cConnections; }
        set { this.cConnections = value; }
     }
     /// <summary>number of controls at this line</summary>
     public UInt32 Controls
     {
        get { return this.cControls; }
        set { this.cControls = value; }
     }
     /// <summary></summary>
     public string ShortName
     {
        get { return this.szShortName; }
        set { this.szShortName = value; }
     }
     /// <summary></summary>
     public string Name
     {
        get { return this.szName; }
        set { this.szName = value; }
     }

     #endregion
}

[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi, Pack = 2)]
public struct MIXERLINETARGET
{
     private UInt32 dwType;
     private UInt32 dwDeviceID;
     private UInt16 wMid;
     private UInt16 wPid;
     private UInt32 vDriverVersion;
     [MarshalAs(UnmanagedType.ByValTStr, SizeConst = MixerXPNative.MAXPNAMELEN)]
     private string szPname;

     #region Properties

     /// <summary>MIXERLINE_TARGETTYPE_xxxx</summary>
     public MIXERLINE_TARGETTYPE Type
     {
        get { return (MIXERLINE_TARGETTYPE)this.dwType; }
        set { this.dwType = (UInt32)value; }
     }
     /// <summary>target device ID of device type</summary>
     public UInt32 DeviceID
     {
        get { return this.dwDeviceID; }
        set { this.dwDeviceID = value; }
     }
     /// <summary>of target device</summary>
     public UInt16 ManufacturerID
     {
        get { return this.wMid; }
        set { this.wMid = value; }
     }
     /// <summary></summary>
     public UInt16 ProductID
     {
        get { return this.wPid; }
        set { this.wPid = value; }
     }
     /// <summary></summary>
     public UInt32 DriverVersion
     {
        get { return this.vDriverVersion; }
        set { this.vDriverVersion = value; }
     }
     /// <summary></summary>
     public string PName
     {
        get { return this.szPname; }
        set { this.szPname = value; }
     }

     #endregion
}
```

## VB Definition:
```cs
Structure MIXERLINE
  Dim cbStruct As UInteger
  Dim dwDestination As UInteger
  Dim dwSource As UInteger
  Dim dwLineID As UInteger
  Dim fdwLine As AudioLineStatus
  Dim dwUser As IntPtr
  Dim dwComponentType As MixerLineComponentType
  Dim cChannels As UInteger
  Dim cConnections As UInteger
  Dim cControls As UInteger
  <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=MIXER_SHORT_NAME_CHARS)> Dim szShortName As String
  <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=MIXER_LONG_NAME_CHARS)> Dim sxName As String
  Dim Target As MIXERLINETARGET
End Structure
```

## Sample Code:
```cs
public enum MIXERLINE_TARGETTYPE : uint
{
     UNDEFINED      = 0,
     WAVEOUT    = 1,
     WAVEIN     = 2,
     MIDIOUT    = 3,
     MIDIIN     = 4,
     AUX        = 5,
}
public enum MIXERLINE_LINEF : uint
{
     ACTIVE          = 0x00000001u,
     DISCONNECTED    = 0x00008000u,
     SOURCE          = 0x80000000u,
}
public enum MIXERLINE_COMPONENTTYPE : uint
{
     DST_FIRST       = 0x00000000u,
     DST_UNDEFINED   = (DST_FIRST + 0),
     DST_DIGITAL     = (DST_FIRST + 1),
     DST_LINE    = (DST_FIRST + 2),
     DST_MONITOR     = (DST_FIRST + 3),
     DST_SPEAKERS    = (DST_FIRST + 4),
     DST_HEADPHONES  = (DST_FIRST + 5),
     DST_TELEPHONE   = (DST_FIRST + 6),
     DST_WAVEIN      = (DST_FIRST + 7),
     DST_VOICEIN     = (DST_FIRST + 8),
     DST_LAST    = (DST_FIRST + 8),
     SRC_FIRST       = 0x00001000u,
     SRC_UNDEFINED   = (SRC_FIRST + 0),
     SRC_DIGITAL     = (SRC_FIRST + 1),
     SRC_LINE    = (SRC_FIRST + 2),
     SRC_MICROPHONE  = (SRC_FIRST + 3),
     SRC_SYNTHESIZER = (SRC_FIRST + 4),
     SRC_COMPACTDISC = (SRC_FIRST + 5),
     SRC_TELEPHONE   = (SRC_FIRST + 6),
     SRC_PCSPEAKER   = (SRC_FIRST + 7),
     SRC_WAVEOUT     = (SRC_FIRST + 8),
     SRC_AUXILIARY   = (SRC_FIRST + 9),
     SRC_ANALOG      = (SRC_FIRST + 10),
     SRC_LAST    = (SRC_FIRST + 10),
}
```
