
## C# Signature:
```cs
[DllImport("winmm.dll", SetLastError=true)]
static extern TODO mixerGetID(TODO);
```

## VB Signature:
```cs
<DllImport("winmm.dll")> _
Shared Function mixerGetID(<MarshalAs(UnmanagedType.I4)> ByVal hmxobj As Integer, ByRef puMxId As UInteger, ByVal fdwId As MixerFlags) As MMRESULT
```
