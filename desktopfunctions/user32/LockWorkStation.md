
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError = true)]
static extern bool LockWorkStation();
```

## VB Signature:
```cs
<DllImport("user32.dll", SetLastError:=True)> _
Public Shared Function LockWorkStation() As Boolean
End Function
```

## Sample Code:
```cs
void LockWorkStationSafe()
    {
        bool result = LockWorkStation();

        if( result == false )
        {
        // An error occured
        throw new Win32Exception( Marshal.GetLastWin32Error() );
        }
    }
```
