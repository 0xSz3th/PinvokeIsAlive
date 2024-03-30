
## C# Signature:
```cs
[DllImport("winscard.dll")]
static extern int SCardEstablishContext(uint dwScope, IntPtr pvReserved1, IntPtr pvReserved2, out IntPtr phContext);
```

## VB Signature:
```cs
<DllImport("winscard.dll")> _
Public Shared Function SCardEstablishContext(dwScope as UInteger, pvReserved1 as IntPtr,  pvReserved2 as IntPtr, <out>() phContext as IntPtr) As Integer

--- Alternatively ---
Enum SCardScope As UInteger
     <Description("User context and and database operations within the domain of the user")>
     SCARD_SCOPE_USER = 0
     <Description("Terminal context. Calling app must have permissions for database action")>
     SCARD_SCOPE_TERMINAL = 1
     <Description("System context. Calling app must have permissions for database action")>
     SCARD_SCOPE_SYSTEM = 2
End Enum
<DllImport("winscard.dll")> _
Public Shared Function SCardEstablishContext(dwScope as SCardScope, pvReserved1 as IntPtr,  pvReserved2 as IntPtr, ByRef phContext as IntPtr) As Integer
End Function
```

## Notes:
```cs
#define SCARD_SCOPE_USER     0    // The context is a user context, and any
                // database operations are performed within the
                // domain of the user.
#define SCARD_SCOPE_TERMINAL 1    // The context is that of the current terminal,
                // and any database operations are performed
                // within the domain of that terminal.  (The
                // calling application must have appropriate
                // access permissions for any database actions.)
#define SCARD_SCOPE_SYSTEM   2    // The context is the system context, and any
                // database operations are performed within the
                // domain of the system.  (The calling
                // application must have appropriate access
                // permissions for any database actions.)
```

## Sample Code:
```cs
static class SmartCard
    {

    #region Win32
    // WinSCard APIs to be imported.
    [DllImport("WinScard.dll")]
    static extern int SCardEstablishContext(uint dwScope,
    IntPtr notUsed1,
    IntPtr notUsed2,
    out IntPtr phContext);

    [DllImport("WinScard.dll")]
    static extern int SCardReleaseContext(IntPtr phContext);

    [DllImport("WinScard.dll")]
    static extern int SCardConnect(IntPtr hContext,
    string cReaderName,
    uint dwShareMode,
    uint dwPrefProtocol,
    ref IntPtr phCard,
    ref IntPtr ActiveProtocol);

    [DllImport("WinScard.dll")]
    static extern int SCardDisconnect(IntPtr hCard, int Disposition);

    // [DllImport("WinScard.dll")]
    // static extern int SCardListReaderGroups(IntPtr hContext,
    // ref string cGroups,
    // ref int nStringSize);

    [DllImport("WinScard.dll", EntryPoint = "SCardListReadersA", CharSet = CharSet.Ansi)]
    static extern int SCardListReaders(
      IntPtr hContext,
      byte[] mszGroups,
      byte[] mszReaders,
      ref UInt32 pcchReaders
      );

    // [DllImport("WinScard.dll")]
    // static extern int SCardFreeMemory(IntPtr hContext,
    // string cResourceToFree);
```

## Sample Code:
```cs
#endregion
```

## Sample Code:
```cs
internal static bool SmartCardInserted()
    {
        bool cardInserted = false;
        IntPtr hContext = IntPtr.Zero;

        try
        {

        List<string> readersList = new List<string>();

        int ret = 0;
        uint pcchReaders = 0;
        int nullindex = -1;
        char nullchar = (char)0;

        // Establish context.
        ret = SCardEstablishContext(2, IntPtr.Zero, IntPtr.Zero, out hContext);

        // First call with 3rd parameter set to null gets readers buffer length.
        ret = SCardListReaders(hContext, null, null, ref pcchReaders);

        byte[] mszReaders = new byte[pcchReaders];

        // Fill readers buffer with second call.
        ret = SCardListReaders(hContext, null, mszReaders, ref pcchReaders);

        // Populate List with readers.
        ASCIIEncoding ascii = new ASCIIEncoding();

        string currbuff = ascii.GetString(mszReaders);

        int len = (int)pcchReaders;

        if (len > 0)
        {
            while (currbuff[0] != nullchar)
            {
            nullindex = currbuff.IndexOf(nullchar);   // Get null end character.
            string reader = currbuff.Substring(0, nullindex);
            readersList.Add(reader);
            len = len - (reader.Length + 1);
            currbuff = currbuff.Substring(nullindex + 1, len);
            }
        }

        // We have list of readers, check for cards.
        IntPtr phCard = IntPtr.Zero;
        IntPtr ActiveProtocol = IntPtr.Zero;
        int result = 0;

        foreach (string readerName in readersList)
        {
            try
            {
            result = SCardConnect(hContext, readerName, 2, 3, ref phCard, ref ActiveProtocol);
            if (result == 0)
            {
                cardInserted = true;
                break;
            }
            }
            finally
            {
            SCardDisconnect(phCard, 0);
            }
        }
        }
        finally
        {
        SCardReleaseContext(hContext);
        }

        return cardInserted;

    } 
    }
```
