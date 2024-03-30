
## C# Signature:
```cs
[DllImport("winmm.dll", SetLastError=true)]
static extern uint waveInReset(IntPtr hwi);
```

## VB Signature:
```cs
<DllImport("winmm.dll")> _
Shared Function waveInReset(<MarshalAs(UnmanagedType.I4)> ByVal hwi As Integer) As MMRESULT
End Function
```
