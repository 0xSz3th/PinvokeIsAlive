
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern int GetMessage(out MSG lpMsg, IntPtr hWnd, uint wMsgFilterMin,
   uint wMsgFilterMax);
```

## VB Signature:
```cs
<DllImport("user32.dll")> _
Public Shared Function GetMessage( _
     ByRef lpMsg As MSG, _
     ByVal hWnd As IntPtr, _
     ByVal wMsgFilterMin As UInteger, _
     ByVal wMsgFilterMax As UInteger) As <MarshalAs(UnmanagedType.Bool)> Boolean
End Function
```

## Notes:
```cs
BOOL GetMessage(
     LPMSG lpMsg,    // address of structure with message
     HWND hWnd,      // handle of window
     UINT wMsgFilterMin, // first message
     UINT wMsgFilterMax  // last message
);
```

## Notes:
```cs
lpMsg
```

## Notes:
```cs
hWnd
```

## Sample Code:
```cs
MSG msg;
int ret;
while((ret = GetMessage(out msg, IntPtr.Zero, 0, 0)) != 0)
{
    if (ret == -1)
    {
       //-1 indicates an error
    }
    else
    {
       TranslateMessage(ref msg);
       DispatchMessage(ref msg);
    }
}
```
