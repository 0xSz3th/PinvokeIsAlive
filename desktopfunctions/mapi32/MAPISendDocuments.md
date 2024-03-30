
## C# Signature:
```cs
/// <summary>
  /// The MAPISendDocuments function sends a standard message with one or more attached files and a cover note. 
  /// 
  /// The cover note is a dialog box that allows the user to enter a list of recipients and an optional 
  /// message. MAPISendDocuments differs from the MAPISendMail function in that it allows 
  /// less flexibility in message generation.
  /// </summary>
  [DllImport("MAPI32.DLL", CharSet=CharSet.Ansi)]
  public static extern uint MAPISendDocuments(IntPtr ulUIParam, string lpszDelimChar, string lpszFullPaths,
    string lpszFileNames, uint ulReserved);
```

## VB Signature:
```cs
Please add!
```
