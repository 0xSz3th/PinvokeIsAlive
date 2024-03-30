
## C# Signature:
```cs
/// <summary>
/// The MAPILogoff function ends a session with the messaging system.
/// </summary>
[DllImport("MAPI32.DLL", CharSet=CharSet.Ansi)]
private static extern uint MAPILogoff(IntPtr lhSession, IntPtr ulUIParam, uint flFlags, uint ulReserved);
```

## VB Signature:
```cs
''' <summary>
''' The MAPILogoff function ends a session with the messaging system.
''' </summary>
<DllImport("MAPI32.DLL", CharSet:=CharSet.Ansi)> _
Private Shared Function MAPILogoff(ByVal lhSession As IntPtr, ByVal ulUIParam As IntPtr, ByVal flFlags As UInteger, ByVal ulReserved As UInteger) As UInteger
End Function
```

## C# Sample Code:
```cs
public void Logoff()
{
    if(sessionPtr != IntPtr.Zero )
    {
        errorCode = MAPILogoff( session, parentWindowPtr , 0, 0 );
        sessionPtr = IntPtr.Zero;
    }
}
```

## VB.NET Sample Code:
```cs
Public Sub Logoff()
    If sessionPtr <> IntPtr.Zero Then
        errorCode = MAPILogoff(session, parentWindowPtr, 0, 0)
        sessionPtr = IntPtr.Zero
    End If
End Sub
```
