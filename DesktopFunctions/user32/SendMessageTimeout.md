
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError=true, CharSet=CharSet.Auto)]
public static extern IntPtr SendMessageTimeout(
    IntPtr hWnd,
    uint Msg, 
    UIntPtr wParam,
    IntPtr lParam, 
    SendMessageTimeoutFlags fuFlags, 
    uint uTimeout, 
    out UIntPtr lpdwResult);

[DllImport("user32.dll", SetLastError=true, CharSet=CharSet.Auto)]
public static extern IntPtr SendMessageTimeout(
    IntPtr windowHandle, 
    uint Msg, 
    IntPtr wParam, 
    IntPtr lParam, 
    SendMessageTimeoutFlags flags, 
    uint timeout, 
    out IntPtr result);

/* Version specifically setup for use with WM_GETTEXT message */

[DllImport("user32.dll", EntryPoint = "SendMessageTimeout", SetLastError=true, CharSet=CharSet.Auto)]
public static extern uint SendMessageTimeoutText(
    IntPtr hWnd, 
    int Msg,              // Use WM_GETTEXT
    int countOfChars, 
    StringBuilder text, 
    SendMessageTimeoutFlags flags, 
    uint uTImeoutj, 
    out IntPtr result);
```

## VB Signature:
```cs
<DllImport("user32.dll", SetLastError:=True)> _
Public Sub SendMessageTimeout(ByVal windowHandle As IntPtr,ByVal Msg As Integer,ByVal wParam As IntPtr,ByVal lParam As IntPtr,ByVal flags As SendMessageTimeoutFlags,ByVal timeout As Integer,ByRef result As IntPtr)
End Sub

<DllImport("user32.dll", SetLastError:=True)> _
Public Shared Function SendMessageTimeout(ByVal windowHandle As IntPtr, ByVal Msg As Integer, ByVal wParam As IntPtr, ByVal lParam As IntPtr, ByVal flags As SendMessageTimeoutFlags, ByVal timeout As Integer, ByRef result As IntPtr) As IntPtr
End Function
```

## Sample Code:
```cs
//Register the message
lMsg = Win32.RegisterWindowMessage("WM_HTML_GETOBJECT");
//Get the object
Win32.SendMessageTimeout(windowHandle, lMsg, IntPtr.Zero, IntPtr.Zero, SendMessageTimeoutFlags.SMTO_ABORT_IF_HUNG, 1000, out lRes);
if(lRes != IntPtr.Zero)
{
    //Get the object from lRes
    htmlDoc= (mshtml.IHTMLDocument)Win32.ObjectFromLresult(lRes, IID_IHTMLDocument, IntPtr.Zero);
    return htmlDoc;
}
```
