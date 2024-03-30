
## C# Signature:
```cs
[DllImport("winmm.dll", SetLastError = true)]
    private static extern MMRESULT midiInGetDevCaps(UIntPtr uDeviceID, ref MIDIINCAPS caps, uint cbMidiInCaps);
```

## Sample Code:
```cs
public void GetInputDevices()
        {
        uint inDevs = midiInGetNumDevs();
        if (inDevs > 0)
        {
            for (int x = 0; x < inDevs; x++)
            {
            MIDIINCAPS caps = new MIDIINCAPS();
            midiInGetDevCaps((UIntPtr)x, ref caps, (uint)Marshal.SizeOf(typeof(MIDIINCAPS)));

            //Do whatever you want with the caps object here
            MessageBox.Show(caps.szPname);
            }
            return;
        }
        MessageBox.Show("No MIDI Input Devices Detected");
        }
    }
```
