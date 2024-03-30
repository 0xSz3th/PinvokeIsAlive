
## C# Signature:
```cs
[DllImport("winmm.dll")]
    static extern uint midiOutOpen(out IntPtr lphMidiOut, uint uDeviceID, IntPtr dwCallback, IntPtr dwInstance, uint dwFlags);
```

## VB Signature:
```cs
<DllImport("winmm.dll")> Shared Function midiOutOpen(ByRef lphMidiOut As IntPtr, ByVal uDeviceID As UInteger, ByVal dwCallback As IntPtr, ByVal dwInstance As IntPtr, ByVal dwFlags As UInteger) As UInteger
    End Function
```
