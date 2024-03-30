
## C# Signature:
```cs
[DllImport("winmm.dll", SetLastError = true)]
public static extern MMRESULT midiOutGetDevCaps(UIntPtr uDeviceID, ref MIDIOUTCAPS lpMidiOutCaps, uint cbMidiOutCaps);
```

## Sample Code:
```cs
[DllImport("winmm.dll", SetLastError = true)]
    static extern uint midiOutGetNumDevs();

    [DllImport("Winmm.dll")]
    static extern uint midiInGetNumDevs();

    [StructLayout(LayoutKind.Sequential)]
    struct MIDIOUTCAPS
    {
        public ushort wMid;
        public ushort wPid;
        public uint vDriverVersion;
        [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 32)]
        public string szPname;
        public ushort wTechnology;
        public ushort wVoices;
        public ushort wNotes;
        public ushort wChannelMask;
        public uint dwSupport;
    }

    private void GetOutputDevices()
    {
        uint outDevs = midiOutGetNumDevs();

        for (int x = 0; x < outDevs; x++)
        {
        MIDIOUTCAPS caps = new MIDIOUTCAPS();
        midiOutGetDevCaps((UIntPtr) x, ref caps, (uint)Marshal.SizeOf(typeof(MIDIOUTCAPS)));

           //Do whatever you want with the caps object here
        MessageBox.Show(caps.szPname);
        }
    }
```
