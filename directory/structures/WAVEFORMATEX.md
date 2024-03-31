
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct WaveFormatExtensible
    {
        public ushort wFormatTag;
        public ushort nChannels;
        public uint nSamplesPerSec;
        public uint nAvgBytesPerSec;
        public ushort nBlockAlign;
        public ushort wBitsPerSample;
        public ushort cbSize;

        public ushort wValidBitsPerSample;
        public uint dwChannelMask;
        public Guid SubFormat;       
    }
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential, pack:=1)> Public Structure WAVEFORMATEXTENSIBLE
    Dim Format As WAVEFORMATEX
    'union {
    'WORD  wValidBitsPerSample;
    'WORD  wSamplesPerBlock;
    'WORD  wReserved;
    ';} Samples;
    Dim wUnionSamples As UInt16
    Dim dwChannelMask As UInteger
    Dim SubFormat As Guid
End Structure
```
