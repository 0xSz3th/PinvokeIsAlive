
## C# Signature:
```cs
[DllImport("winmm.dll", SetLastError = true, CharSet = CharSet.Auto)]
  public static extern uint waveOutPrepareHeader(IntPtr hWaveOut, IntPtr pwh, int uSize);
  // Need to use IntPtr as WAVEHEADER struct must be in a fixed memory location. See Tips & Tricks below
```

## VB Signature:
```cs
Declare Function waveOutPrepareHeader Lib "winmm.dll" (TODO) As TODO
```

## Tips & Tricks:
```cs
waveHdrPtr = Marshal.AllocHGlobal(Marshal.SizeOf(waveHdr));
```

## Tips & Tricks:
```cs
waveHdr.lpData = wavedata;  // audio buffer
    waveHdr.dwBufferLength = wf.nSamplesPerSec * wf.nBlockAlign;  // it's size
    waveHdr.dwFlags = 0;    // clear before waveOutPrepareHeader()

    Marshal.StructureToPtr(waveHdr, waveHdrPtr, true);    // copy to unmanaged memory

    if ((MMRESULT = waveOutPrepareHeader(waveDevice, waveHdrPtr, Marshal.SizeOf(waveHdr))) != MMSYSERR_NOERROR)
    {
       waveOutGetErrorText(MMRESULT, errmsg, MAXERRORLENGTH);

       MessageBox.Show(
       "waveOutPrepareHeader(): " + errmsg.ToString(),
        this.Text,
        MessageBoxButtons.OK,
        MessageBoxIcon.Error);

        return;
    }

    WAVEHDR wh = (WAVEHDR)Marshal.PtrToStructure(waveHdrPtr, typeof(WAVEHDR));  // copy struct back from unmanaged memory

    waveHdr = wh;  // reset managed struct

    waveHdr.dwFlags |= (WHDR_BEGINLOOP | WHDR_ENDLOOP);  // add the looping flag bits
    waveHdr.dwLoops = MINUS_ONE; ;

    Marshal.StructureToPtr(waveHdr, waveHdrPtr, true);   // and update the unmanaged struct.
```

## Tips & Tricks:
```cs
if ((MMRESULT = waveOutWrite(waveDevice, waveHdrPtr, Marshal.SizeOf(waveHdr))) != MMSYSERR_NOERROR)
        [snipped]
```

## Tips & Tricks:
```cs
while ((waveHdr.dwFlags & WHDR_DONE) == 0)  // wait for it
    {
       if ((MMRESULT = waveOutReset(waveDevice)) != MMSYSERR_NOERROR)
       {
        waveOutGetErrorText(MMRESULT, errmsg, MAXERRORLENGTH);

        MessageBox.Show(
        "waveOutReset(): " + errmsg.ToString(),
        this.Text,
        MessageBoxButtons.OK,
        MessageBoxIcon.Error);
       }

       WAVEHDR wh = (WAVEHDR)Marshal.PtrToStructure(waveHdrPtr, typeof(WAVEHDR)); // copy unmanaged struct

       waveHdr = wh;  // update managed struct
    }
```

## Tips & Tricks:
```cs
if ((MMRESULT = waveOutUnprepareHeader(waveDevice, waveHdrPtr, Marshal.SizeOf(waveHdr))) != MMSYSERR_NOERROR)
          [snipped]
```

## Tips & Tricks:
```cs
Marshal.FreeHGlobal(waveHdrPtr);
```
