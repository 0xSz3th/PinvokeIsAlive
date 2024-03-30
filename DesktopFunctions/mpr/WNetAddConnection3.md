
## C# Signature:
```cs
/* Uses Struct rather than class version of NETRESOURCE */
[DllImport("mpr.dll")]
private static extern int WNetAddConnection3(IntPtr hWndOwner,
    ref NETRESOURCE lpNetResource, string lpPassword,
    string lpUserName, int dwFlags);
```

## VB .NET Signature:
```cs
''' <summary>
    ''' Use to pass handle to Provider of Network Resource
    ''' </summary>
    ''' <param name="hWndOwner"></param>
    ''' <param name="lpNetResource"></param>
    ''' <param name="lpPassword"></param>
    ''' <param name="lpUserName"></param>
    ''' <param name="dwFlags"></param>
    ''' <returns></returns>
    ''' <remarks></remarks>
    <DllImport("mpr.dll")> _
    Private Shared Function WNetAddConnection3(ByVal hWndOwner As IntPtr, _
                           ByRef lpNetResource As NETRESOURCE, _
                           ByVal lpPassword As String, _
                           ByVal lpUserName As String, _
                           ByVal dwFlags As Integer) As Integer
    End Function
```

## Sample Code:
```cs
private const int RESOURCETYPE_ANY = 0x0;
private const int CONNECT_INTERACTIVE = 0x8;
private const int CONNECT_PROMPT = 0x10;

...

NETRESOURCE ConnInf = new NETRESOURCE();

ConnInf.dwType = RESOURCETYPE_ANY;
ConnInf.RemoteName = @"\\MachineName";

// Allow the user to log onto machine
WNetAddConnection3(hWnd, ref ConnInf, null, null,
    CONNECT_INTERACTIVE | CONNECT_PROMPT);
```
