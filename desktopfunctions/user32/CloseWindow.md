
## C# Signature:
```cs
[return: MarshalAs(UnmanagedType.Bool)]
    [ReliabilityContract(Consistency.WillNotCorruptState, Cer.MayFail)]
    [DllImport("user32", CharSet = CharSet.Unicode, SetLastError = true)]
    public static extern bool CloseWindowStation(IntPtr hWinsta);
```
