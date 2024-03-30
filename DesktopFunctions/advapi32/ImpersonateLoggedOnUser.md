
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError=true)]
static extern bool ImpersonateLoggedOnUser(IntPtr hToken);
```

## VB Signature:
```cs
Declare Function ImpersonateLoggedOnUser Lib "advapi32.dll" (ByVal hToken As Integer) As Integer
```

## Sample Code:
```cs
Public Sub Logon(ByVal strUser As String, ByVal strPassword As String, ByVal strDomain As String)
    Dim lngLogonType, lngLogonProvider, lngTokenHandle As Integer
    Dim blnResult As Boolean

    lngLogonType = LOGON32_LOGON_INTERACTIVE
    lngLogonProvider = LOGON32_PROVIDER_DEFAULT

    blnResult = RevertToSelf()
```

## Sample Code:
```cs
blnResult = LogonUser(strUser, strDomain, strPassword, _
                         lngLogonType, lngLogonProvider, _
                         lngTokenHandle)
    If blnResult Then
        blnResult = ImpersonateLoggedOnUser(lngTokenHandle)
        CloseHandle(lngTokenHandle)
    Else
        MsgBox("Error logging on")
    End If
End Sub
```
