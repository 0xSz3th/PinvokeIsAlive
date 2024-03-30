
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
public struct WAVEHDR
{
  public IntPtr lpData; // pointer to locked data buffer
  public uint dwBufferLength; // length of data buffer
  public uint dwBytesRecorded; // used for input only
  public IntPtr dwUser; // for client's use
  public WaveHdrFlags dwFlags; // assorted flags (see defines)
  public uint dwLoops; // loop control counter
  public IntPtr lpNext; // PWaveHdr, reserved for driver
  public IntPtr reserved; // reserved for driver
}
```

## VB Definition:
```cs
Structure WAVEHDR
  Dim lpData As IntPtr
  Dim dwBufferLength As UInteger
  Dim dwBytesRecorded As UInteger
  Dim dwUser As IntPtr
  Dim dwFlags As WaveHdrFlags
  Dim dwLoops As UInteger
  Dim lpNext As IntPtr
  Dim reserved As UIntPtr
End Structure
```
