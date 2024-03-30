
## C# Signature:
```cs
/// <summary>
  /// The MAPIAddress function creates or modifies a set of address list entries.
  /// </summary>
  [DllImport("MAPI32.DLL", CharSet=CharSet.Ansi)]
  public static extern uint MAPIAddress(IntPtr lhSession, IntPtr ulUIParam, string lpszCaption,
    uint nEditFields, string lpszLabels, uint nRecips, IntPtr lpRecips,
    uint flFlags, uint ulReserved, ref uint lpnNewRecips, ref IntPtr lppNewRecips);
```

## VB Signature:
```cs
Please add!
```
