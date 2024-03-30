
## C# Signature:
```cs
[DllImport("WINSCARD.DLL")]
    internal static extern uint SCardGetStatusChange(IntPtr hContext, UInt32 dwTimeout, [In, Out] SCARD_READERSTATE[] rgReaderStates, UInt32 cReaders);
```

## VB Signature:
```cs
Declare Function WinSCard Lib "winscard.dll" (TODO) As TODO
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi)]
    internal struct SCARD_READERSTATE
    {
    /// <summary>
    /// Reader
    /// </summary>
    internal string szReader;
    /// <summary>
    /// User Data
    /// </summary>
    internal IntPtr pvUserData;
    /// <summary>
    /// Current State
    /// </summary>
    internal UInt32 dwCurrentState;
    /// <summary>
    /// Event State/ New State
    /// </summary>
    internal UInt32 dwEventState;
    /// <summary>
    /// ATR Length
    /// </summary>
    internal UInt32 cbAtr;
    /// <summary>
    /// Card ATR
    /// </summary>
    [MarshalAs(UnmanagedType.ByValArray, SizeConst = 32)]
    internal byte[] rgbAtr;
    }

    And

    internal enum SCardState
    {
    /// <summary>
    /// Unware
    /// </summary>
    UNAWARE = 0x00000000,
    /// <summary>
    /// State Ignored
    /// </summary>
    IGNORE = 0x00000001,
    /// <summary>
    /// State changed
    /// </summary>
    CHANGED = 0x00000002,
    /// <summary>
    /// State Unknown
    /// </summary>
    UNKNOWN = 0x00000004,
    /// <summary>
    /// State Unavilable
    /// </summary>
    UNAVAILABLE = 0x00000008,
    /// <summary>
    /// State empty
    /// </summary>
    EMPTY = 0x00000010,
    /// <summary>
    /// Card Present
    /// </summary>
    PRESENT = 0x00000020,
    /// <summary>
    /// ATR mathched
    /// </summary>
    ATRMATCH = 0x00000040,
    /// <summary>
    /// In exclusive use
    /// </summary>
    EXCLUSIVE = 0x00000080,
    /// <summary>
    /// In use
    /// </summary>
    INUSE = 0x00000100,
    /// <summary>
    /// Mute State
    /// </summary>
    MUTE = 0x00000200,
    /// <summary>
    /// Card unpowered
    /// </summary>
    UNPOWERED = 0x00000400
    }
```
