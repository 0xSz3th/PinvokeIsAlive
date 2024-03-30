
## C# Signature:
```cs
/// <summary>
  /// The MAPIResolveName function transforms a message recipient's name as entered by a user 
  /// to an unambiguous address list entry.
  /// </summary>
  [DllImport("MAPI32.DLL", CharSet=CharSet.Ansi)]
  public static extern uint MAPIResolveName(IntPtr lhSession, IntPtr ulUIParam, string lpszName,
    uint flFlags, uint ulReserved, ref MapiRecipDesc lppRecips);
```

## VB Signature:
```cs
Please add!
```

## Tips & Tricks:
```cs
For some unknown reason, you need to pass lpszName as a new object, not an existing reference, otherwise you get an AccessViolationException.
```

## Sample Code:
```cs
MapiRecipDesc mpd = null;
  MAPIResolveName(lhSessionNull, this.Handle, new String(textbox.Text.ToCharArray()), Mapi.MAPI_DIALOG, 0, ref mpd);
```
