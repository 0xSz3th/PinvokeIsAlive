
## C# Signature:
```cs
[DllImport("winmm.dll")]
static extern UInt32 midiOutLongMsg(IntPtr hmo, IntPtr lpMidiOutHdr, UInt32 cbMidiOutHdr); // LD83
```

## VB Signature:
```cs
Declare Function midiOutLongMsg Lib "winmm.dll" (hmo AS Intptr, lpMidiOutHdr AS Intptr, cbMidiOutHdr AS UInt32) AS UInt32 ' Untested - LD83
```
