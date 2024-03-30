
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
/// <summary>
    /// ACT (reference) code pages.
    /// </summary>
    /// <remarks>
    /// A table of ACT code pages can be found here:
    /// http://msdn.microsoft.com/en-us/library/aa288104.aspx
    /// </remarks>
    private enum ActCodePage
    {
        /// <summary>
        /// Default to ANSI code page
        /// </summary>
        CP_ACP = 0,

        /// <summary>
        /// Default to OEM code page
        /// </summary>
        CP_OEMCP = 1,

        /// <summary>
        /// Mac?
        /// </summary>
        CP_MACCP = 2,

        /// <summary>
        /// Current thread's ANSI code page
        /// </summary>
        CP_THREAD_ACP = 3,

        /// <summary>
        /// SYMBOL translations
        /// </summary>
        CP_SYMBO = 42,

        /// <summary>
        /// Unicode (UTF-7)
        /// </summary>
        CP_UTF7 = 65000,

        /// <summary>
        /// Unicode (UTF-8)
        /// </summary>
        CP_UTF8 = 65001,
    }

    /// <summary>
    /// Gets the .NET Encoding object for a given ACT code page.
    /// </summary>
    /// <param name="codePage">The code page 'pointer' to look up.</param>
    /// <returns>The .NET Encoding for the requested code page.</returns>
    private static Encoding GetEncoding(ActCodePage codePage)
    {
        CPINFOEX info = new CPINFOEX();
        if (GetCPInfoEx((int)codePage, 0, out info))
        {
            Regex findNumber = new Regex(@"^\d+", RegexOptions.Compiled);
            Match match = findNumber.Match(info.CodePageName);
            if (match.Success)
            {
                int cp = int.Parse(match.Groups[0].Value);
                return Encoding.GetEncoding(cp);
            }
            else
            {
                throw new ArgumentException("Unable to find codepage number.");
            }
        }
        else
        {
            throw new Win32Exception(Marshal.GetLastWin32Error());
        }
    }
```
