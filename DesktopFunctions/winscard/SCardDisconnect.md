
## C# Signature:
```cs
[DllImport("winscard.dll")]
static extern int SCardDisconnect(int hCard, int dwDisposition);
```

## VB/NET Signature:
```cs
Enum SCardDisposition As UInt32
    SCARD_LEAVE_CARD = 0
    SCARD_RESET_CARD = 1
    SCARD_UNPOWER_CARD = 2
    SCARD_EJECT_CARD = 3
End Enum
<DllImport("WinScard.dll")>
Public Shared Function SCardDisconnect(hCard As Integer, Disposition As SCardDisposition) As Integer
End Function
```

## User-Defined Types:
```cs
SCARD_LEAVE_CARD = 0 Do nothing on close
   SCARD_RESET_CARD = 1 Reset on close
   SCARD_UNPOWER_CARD = 2 Power down on close
   SCARD_EJECT_CARD = 3 Eject on close
```
