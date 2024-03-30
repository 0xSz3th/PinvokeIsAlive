
## C# Signature:
```cs
[DllImport("winmm.dll", SetLastError = true, CharSet = CharSet.Auto)]
public static extern uint waveOutOpen(ref IntPtr hWaveOut, IntPtr uDeviceID, ref WAVEFORMATEX lpFormat, delegateWaveOutProc dwCallback, IntPtr dwInstance, uint dwFlags);
```

## VB Signature:
```cs
Declare Function waveOutOpen Lib "winmm.dll" Alias "waveOutOpen" (ByRef phwi As IntPtr, ByVal uDeviceID As IntPtr, ByRef pwfx As WAVEFORMATEX, ByVal dwCallback As IntPtr, ByVal dwCallbackInstance As IntPtr, ByVal fdwOpen As WAVE_FLAGS) As MMSYSERR
```

## VB Signature:
```cs
Declare Function waveOutOpen Lib "winmm.dll" Alias "waveOutOpen" (ByRef phwi As IntPtr, ByVal uDeviceID As IntPtr, ByRef pwfx As WAVEFORMATEXTENSIBLE, ByVal dwCallback As IntPtr, ByVal dwCallbackInstance As IntPtr, ByVal fdwOpen As WAVE_FLAGS) As MMSYSERR
```
