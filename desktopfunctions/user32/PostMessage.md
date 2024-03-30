
## C# Signature:
```cs
[return: MarshalAs(UnmanagedType.Bool)]
[DllImport("user32.dll", SetLastError = true, CharSet = CharSet.Auto)]
static extern bool PostMessage(HandleRef hWnd, uint Msg, IntPtr wParam, IntPtr lParam);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", SetLastError:=True, CharSet:=CharSet.Auto)> _
Private Shared Function PostMessage(ByVal hWnd As IntPtr, ByVal Msg As UInteger, ByVal wParam As IntPtr, ByVal lParam As IntPtr) As Boolean
End Function
```

## Oxygene.NET Signature:
```cs
[DllImport("user32.dll", SetLastError := true)]
class method PostMessage(hWnd: IntPtr; Msg: UInt32; wParam, lParam: IntPtr): Boolean; external;
```

## Sample Code:
```cs
void PostMessageSafe( HandleRef hWnd, uint msg, IntPtr wParam, IntPtr lParam )
    {
        bool returnValue = PostMessage( hWnd, msg, wParam, lParam );
        if( !returnValue )
        {
        // An error occured
        throw new Win32Exception( Marshal.GetLastWin32Error() );
        }
    }
```
