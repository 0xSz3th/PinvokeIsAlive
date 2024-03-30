
## C# Signature:
```cs
[ReliabilityContract(Consistency.WillNotCorruptState, Cer.MayFail)]
    [DllImport("user32", CharSet = CharSet.Unicode, SetLastError = true)]
    public static extern SafeWindowStationHandle OpenWindowStation(
        [MarshalAs(UnmanagedType.LPTStr)]
        string lpszWinSta,
        [MarshalAs(UnmanagedType.Bool)]
        bool fInherit,
        AccessMask dwDesiredAccess
    );
```

## User-Defined Types:
```cs
public sealed class SafeWindowStationHandle : SafeHandleZeroOrMinusOneIsInvalid
{
    public SafeWindowStationHandle()
        : base(true)
    {
    }

    protected override bool ReleaseHandle()
    {
        return SafeNativeMethods.CloseWindowStation(handle);
    }
}
```
