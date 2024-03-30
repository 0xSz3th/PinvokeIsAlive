
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern bool GetDeviceGammaRamp(IntPtr hdc, IntPtr lpRamp);
```

## Sample Code:
```cs
[DllImport("gdi32.dll")]
    public static extern int GetDeviceGammaRamp(IntPtr hDC, ref RAMP lpRamp);

    [DllImport("gdi32.dll")]
    public static extern int SetDeviceGammaRamp(IntPtr hDC, ref RAMP lpRamp);

    [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Ansi)] 
    public struct RAMP
    {
        [ MarshalAs(UnmanagedType.ByValArray, SizeConst=256)] 
        public UInt16[] Red;
        [ MarshalAs(UnmanagedType.ByValArray, SizeConst=256)] 
        public UInt16[] Green;
        [ MarshalAs(UnmanagedType.ByValArray, SizeConst=256)] 
        public UInt16[] Blue;
    }
```
