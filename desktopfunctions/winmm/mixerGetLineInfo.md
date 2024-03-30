
## C# Signature:
```cs
[DllImport("winmm.dll")]
static extern Int32 mixerGetLineInfo(IntPtr hmxobj,
   ref MIXERLINE pmxl, UInt32 fdwInfo);
```

## VB Signature:
```cs
<DllImport("winmm.dll")> _
Shared Function mixerGetLineInfo(<MarshalAs(UnmanagedType.I4)> ByVal hmxobj As Integer, ByRef pmxl As MIXERLINE, ByVal fdwInfo As MixerFlags) As MMRESULT
  End Function
```

## Tips & Tricks:
```cs
[DllImport("winmm.dll")]
private static extern Int32 mixerGetLineInfo(IntPtr hmxobj, ref MIXERLINE pmxl, uint fdwInfo);

public static Int32 mixerGetLineInfo(IntPtr hmxobj, ref MIXERLINE pmxl, MIXER_OBJECTF fdwInfo, MIXER_GETLINEINFOF fieldToFollow)
{
     uint flags = ((uint)fdwInfo | (uint)fieldToFollow);
     return mixerGetLineInfo(hmxobj, ref pmxl, flags);
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

public enum MIXER_GETLINEINFOF : uint
{
     DESTINATION      = 0x00000000u,
     SOURCE       = 0x00000001u,
     LINEID       = 0x00000002u,
     COMPONENTTYPE    = 0x00000003u,
     TARGETTYPE       = 0x00000004u,
     QUERYMASK    = 0x0000000Fu,
}
```
