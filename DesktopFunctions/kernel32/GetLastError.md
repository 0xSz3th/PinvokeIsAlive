
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern uint GetLastError();
// GetLastError is save!
```

## C# Signature:
```cs
// You should never PInvoke to GetLastError.  Call Marshal.GetLastWin32Error instead!
```

## VB Signature:
```cs
' You should never PInvoke to GetLastError.  Call Marshal.GetLastWin32Error instead!
```

## Boo Signature:
```cs
[DllImport("kernel32.dll")]
def GetLastError() as int:
     pass
```

## Notes:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
    static extern bool CloseHandle(IntPtr hObject);
```
