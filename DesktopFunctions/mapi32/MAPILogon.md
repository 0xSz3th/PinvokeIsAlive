
## C# Signature:
```cs
/// <summary>
  /// The MAPILogon function begins a Simple MAPI session, loading the default message store 
  /// and address book providers.
  /// </summary>
  [DllImport("MAPI32.DLL", CharSet=CharSet.Ansi)]
  public static extern uint MAPILogon(IntPtr ulUIParam, string lpszProfileName, string lpszPassword, 
    uint flFlags, uint ulReserved, ref IntPtr lplhSession);
```

## VB Signature:
```cs
<DllImport("MAPI32.dll", SetLastError:=True)> _
    Private Shared Function MAPILogon(ByVal uiParam As Integer, _
                      ByVal user As String, _
                      ByVal password As String, _
                      ByVal flags As Integer, _
                      ByVal reserved As Integer, _
                      ByRef session As Integer) As Integer
    End Function
```

## Sample Code:
```cs
uint error = MAPILogon(hwnd, null, null, MAPI_LOGON_UI, 0, ref session);
  return error == 0;
```
