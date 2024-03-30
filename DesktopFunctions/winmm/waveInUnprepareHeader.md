
## C# Signature:
```cs
[DllImport("winmm.dll", SetLastError=true)]
static extern MMRESULT waveInUnprepareHeader(IntPtr hwi, ref WAVEHDR pwh, uint cbwh);
```

## VB Signature:
```cs
<DllImport("winmm.dll")> _
Shared Function waveInUnprepareHeader(<MarshalAs(UnmanagedType.I4)> ByVal hwi As Integer, ByVal pwh As IntPtr, ByVal cbwh As UInteger) As MMRESULT
End Function
<DllImport("winmm.dll")> _
Shared Function waveInUnprepareHeader(<MarshalAs(UnmanagedType.I4)> ByVal hwi As Integer, ByRef pwh As WAVEHDR, ByVal cbwh As UInteger) As MMRESULT
End Function
```
