
## C# Signature:
```cs
[DllImport("winscard.dll", EntryPoint="SCardConnect", CharSet=CharSet.Auto)]
static extern int SCardConnect(
     int hContext, 
     [MarshalAs(UnmanagedType.LPTStr)] string szReader, //I was getting SCARD_E_UNKNOWN_READER until i removed [MarshalAs(UnmanagedType.LPTStr)]
     UInt32 dwShareMode, 
     UInt32 dwPreferredProtocols, 
     out int phCard, 
     out UInt32 pdwActiveProtocol);
```

## Sample Code:
```cs
SCARDCONTEXT hContext;
SCARDHANDLE hCard;
DWORD dwActiveProtocol;
LONG rv;

rv = SCardEstablishContext(SCARD_SCOPE_SYSTEM, NULL, NULL, &hContext);
rv = SCardConnect(hContext, "Reader X", SCARD_SHARE_SHARED,
    SCARD_PROTOCOL_T0, &hCard, &dwActiveProtocol);
```
