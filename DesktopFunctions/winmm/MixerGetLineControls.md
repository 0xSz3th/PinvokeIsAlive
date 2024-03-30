
## C# Signature:
```cs
[DllImport("winmm.dll")]
static extern Int32 mixerGetLineControls(IntPtr hmxobj,
   ref MIXERLINECONTROLS pmxlc, UInt32 fdwControls);
```

## VB Signature:
```cs
Declare Function mixerGetLineControls Lib "winmm.dll" (hmxobj As IntPtr, _
   ByRef pmxlc As MIXERLINECONTROLS, fdwControls As Integer) As Integer
```

## Tips & Tricks:
```cs
[DllImport("winmm.dll")]
private static extern Int32 mixerGetLineControls(IntPtr hmxobj, ref MIXERLINECONTROLS pmxlc, uint fdwControls);

public static Int32 mixerGetLineControls(IntPtr hmxobj, ref MIXERLINECONTROLS pmxlc, MIXER_OBJECTF mixerFlags, MIXER_GETLINECONTROLSF controlsFlags)
{
     uint flags = ((uint)mixerFlags | (uint)controlsFlags);
     return mixerGetLineControls(hmxobj, ref pmxlc, flags);
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
public enum MIXER_GETLINECONTROLSF : uint
{
     ALL      = 0x00000000u,
     ONEBYID      = 0x00000001u,
     ONEBYTYPE    = 0x00000002u,

     QUERYMASK    = 0x0000000Fu,
}
```
