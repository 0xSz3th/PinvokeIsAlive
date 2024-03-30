
## C# Signature:
```cs
/// <summary>
  /// The MAPISaveMail function saves a message into the message store.
  /// </summary>
  [DllImport("MAPI32.DLL", CharSet=CharSet.Ansi)]
  public static extern uint MAPISaveMail(IntPtr lhSession, IntPtr ulUIParam,
    MapiMessage lpMessage, uint flFlags, uint ulReserved, string lpszMessageID);
```

## VB Signature:
```cs
Please add!
```
