
## C# Signature:
```cs
/// <summary>
    /// Gets information on a named code page.
    /// </summary>
    /// <param name="CodePage">The code page number.</param>
    /// <param name="dwFlags">Reserved.  Must be 0.</param>
    /// <param name="lpCPInfoEx">The CPINFOEX struct to initialize.</param>
    /// <returns><c>true</c> if the operation completed successfully; <c>false</c> otherwise.</returns>
    [DllImport("kernel32.dll", SetLastError = true)]
    private static extern bool GetCPInfoEx([MarshalAs(UnmanagedType.U4)] int CodePage, [MarshalAs(UnmanagedType.U4)] int dwFlags, out CPINFOEX lpCPInfoEx);
```

## User-Defined Types:
```cs
private const int MAX_DEFAULTCHAR = 2;
    private const int MAX_LEADBYTES = 12;
    private const int MAX_PATH = 260;

    [StructLayout(LayoutKind.Sequential)]
    private struct CPINFOEX
    {
        [MarshalAs(UnmanagedType.U4)]
        public int MaxCharSize;

        [MarshalAs(UnmanagedType.ByValArray, SizeConst = MAX_DEFAULTCHAR)]
        public byte[] DefaultChar;

        [MarshalAs(UnmanagedType.ByValArray, SizeConst = MAX_LEADBYTES)]
        public byte[] LeadBytes;

        public char UnicodeDefaultChar;

        [MarshalAs(UnmanagedType.U4)]
        public int CodePage;

        [MarshalAs(UnmanagedType.ByValTStr, SizeConst = MAX_PATH)]
        public string CodePageName;
    }
```

## Sample Code:
```cs
private enum ActCodePage
    {
        CP_ACP = 0,
        CP_OEMCP = 1,
        CP_MACCP = 2,
    }
```
