
## C# Signature:
```cs
[StructLayout(LayoutKind.Sequential)]
    internal struct MIDIHDR
    {
    public IntPtr data;
    public uint bufferLength;
    public uint bytesRecorded;
    public IntPtr user;
    public uint flags;
    public IntPtr next;
    public IntPtr reserved;
    public uint offset;
    [MarshalAs(UnmanagedType.ByValArray, SizeConst = 4)]
    public IntPtr[] reservedArray;
    }
```

## VB Signature:
```cs
Declare Function MIDIHDR Lib "winmm.dll" (TODO) As TODO
```
