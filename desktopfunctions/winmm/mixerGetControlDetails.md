
## C# Signature:
```cs
[DllImport("winmm.dll")]
static extern Int32 mixerGetControlDetails(IntPtr hmxobj,
   ref MixerControlDetails pmxcd, UInt32 fdwDetailsmixer);
```

## VB Signature:
```cs
Declare Function mixerGetControlDetails Lib "winmm.dll" (<MarshalAs(UnmanagedType.I4)> ByVal hmxobj As Integer, ByRef pmxcd As MIXERCONTROLDETAILS, ByVal fdwDetails As Integer) As Integer
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi, Pack = 4)]
public struct MIXERCONTROLDETAILS
{
     private UInt32 cbStruct;
     private UInt32 dwControlID;
     private UInt32 cChannels;
     private IntPtr hwndOwner;
//     private UInt32 cMultipleItems; //Unioned with hwndOwner /* if _MULTIPLE, the number of items per channel */
     private UInt32 cbDetails;
     private IntPtr paDetails;

     #region Properties

     /// <summary>size in bytes of MIXERCONTROLDETAILS</summary>
     public UInt32 StructSize
     {
        get { return this.cbStruct; }
        set { this.cbStruct = value; }
     }
     /// <summary>control id to get/set details on</summary>
     public UInt32 ControlID
     {
        get { return this.dwControlID; }
        set { this.dwControlID = value; }
     }
     /// <summary>number of channels in paDetails array</summary>
     public UInt32 Channels
     {
        get { return this.cChannels; }
        set { this.cChannels = value; }
     }
     /// <summary>for MIXER_SETCONTROLDETAILSF_CUSTOM</summary>
     public IntPtr OwnerHandle
     {
        get { return this.hwndOwner; }
        set { this.hwndOwner = value; }
     }
     /// <summary>if _MULTIPLE, the number of items per channel</summary>
     public UInt32 MultipleItems
     {
        get { return (UInt32)this.hwndOwner; }
        set { this.hwndOwner = (IntPtr)value; }
     }
     /// <summary>size of _one_ details_XX struct</summary>
     public UInt32 DetailsItemSize
     {
        get { return this.cbDetails; }
        set { this.cbDetails = value; }
     }
     /// <summary>pointer to array of details_XX structs</summary>
     public IntPtr DetailsPointer
     {
        get { return this.paDetails; }
        set { this.paDetails = value; }
     }

     #endregion
}
```

## Tips & Tricks:
```cs
[DllImport("winmm.dll", CharSet = CharSet.Unicode)]
private static extern Int32 mixerGetControlDetails(IntPtr hmxobj, ref MIXERCONTROLDETAILS pmxcd, uint fdwDetails);

public static Int32 mixerGetControlDetails(IntPtr hmxobj, ref MIXERCONTROLDETAILS pmxcd, MIXER_OBJECTF fdwDetails, MIXER_GETCONTROLDETAILSF getControlDetails)
{
     uint flags = ((uint)fdwDetails | (uint)getControlDetails);
     return mixerGetControlDetails(hmxobj, ref pmxcd, flags);
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
public enum MIXER_GETCONTROLDETAILSF : uint
{
     VALUE      = 0x00000000u,
     LISTTEXT   = 0x00000001u,

     QUERYMASK  = 0x0000000Fu,
}
```
