
## C# Signature:
```cs
/// <summary>
  /// The MAPIReadMail function retrieves a message for reading.
  /// </summary>
  [DllImport("MAPI32.DLL", CharSet=CharSet.Ansi)]
  public static extern uint MAPIReadMail(IntPtr lhSession, IntPtr ulUIParam, string lpszMessageID,
    uint flFlags, uint ulReserved, ref IntPtr lppMessage);
```

## VB Signature:
```cs
<Runtime.InteropServices.DllImport("MAPI32.DLL", CharSet:=System.Runtime.InteropServices.CharSet.Ansi)> _
   Public Shared Function MAPIReadMail(ByVal lhSession As IntPtr, ByVal ulUIParam As IntPtr, ByVal lpszMessageID As String, 
   ByVal flFlags As UInteger, ByVal ulReserved As UInteger, ByRef lppMessage As IntPtr) As UInteger
   End Function
```
