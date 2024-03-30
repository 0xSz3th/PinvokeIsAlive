
## C# Signature:
```cs
/// <summary>
  /// The MAPIFindNext function retrieves the next (or first) message identifier of a specified type 
  /// of incoming message.
  /// </summary>
  [DllImport("MAPI32.DLL", CharSet=CharSet.Ansi)]
  public static extern uint MAPIFindNext(IntPtr lhSession, IntPtr ulUIParam, string lpszMessageType,
    string lpszSeedMessageID, uint flFlags, uint ulReserved, StringBuilder lpszMessageID);
```

## VB Signature:
```cs
Please add!
```
