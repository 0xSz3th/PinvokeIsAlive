
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool ExitWindowsEx(ExitWindows uFlags, ShutdownReason dwReason);
```

## Alternative C# Signature:
```cs
[DllImport("user32.dll", SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool ExitWindowsEx(uint uFlags, uint dwReason);
```

## VB Signature:
```cs
<DllImport("user32.dll", SetLastError:=True)> _
Shared Function ExitWindowsEx( _
     ByVal uFlags As ExitWindows, _
     ByVal dwReason As ShutdownReason) As <MarshalAs(UnmanagedType.Bool)> Boolean
End Function
```

## Alternative VB Signature:
```cs
Declare Function ExitWindowsEx Lib "user32" (ByVal dwOptions As Int32, ByVal dwReserved As Int32) As Int32
```

## Sample Code:
```cs
class Class1
    {
        [DllImport("user32.dll")]
        static extern bool ExitWindowsEx(uint uFlags, uint dwReason);

        [STAThread]
        static void Main(string[] args)
        {
            ExitWindowsEx(ExitWindows.LogOff, ShutdownReason.MajorOther | ShutdownReason.MinorOther); 
            //this will cause the computer to logoff.
        }
    }
```
