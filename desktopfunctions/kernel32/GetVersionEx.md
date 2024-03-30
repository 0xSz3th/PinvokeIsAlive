
## C# Signatures:
```cs
// This must be used if OSVERSIONINFO is defined as a struct or Class - The previous [In,Out] parameter defined for
```

## C# Signatures:
```cs
[ DllImport( "kernel32" )] 
static extern bool GetVersionEx( ref OSVERSIONINFO osvi );
```

## VB.Net Signatures:
```cs
<DllImport("kernel32")> _
Private Shared Function GetVersionEx(ByRef osvi As OSVERSIONINFO) As Boolean
End Function

' This must be used if OSVERSIONINFO is defined as a class
<DllImport("kernel32")> _
Private Shared Function GetVersionEx(<[In](), Out()> ByVal osvi As OSVERSIONINFO) As Boolean
End Function
```

## Sample Code:
```cs
Console.WriteLine( "\nPassing OSVERSIONINFO as class" );

OSVERSIONINFO osvi = new OSVERSIONINFO();
osvi.OSVersionInfoSize = Marshal.SizeOf( osvi );

GetVersionEx( osvi );

Console.WriteLine( "Class size:    {0}", osvi.OSVersionInfoSize );
```

## Sample Code:
```cs
Console.WriteLine( "\nPassing OSVERSIONINFO as struct" );

OSVERSIONINFO osvi2 = new OSVERSIONINFO();
osvi2.OSVersionInfoSize = Marshal.SizeOf(ref typeof(OSVERSIONINFO) );

GetVersionEx( ref osvi2 );

Console.WriteLine( "Struct size:   {0}", osvi2.OSVersionInfoSize );
```

## Alternative Managed API:
```cs
Friend Function IsWinVista() As Boolean
    Dim osInfo As System.OperatingSystem = System.Environment.OSVersion
    Return (osInfo.Platform = PlatformID.Win32NT AndAlso osInfo.Version.Major = 6)
    End Function

    Friend Function IsWinXP() As Boolean
    Dim osInfo As System.OperatingSystem = System.Environment.OSVersion
    Return (osInfo.Platform = PlatformID.Win32NT AndAlso osInfo.Version.Major = 5 AndAlso osInfo.Version.Minor >= 1)
    End Function
```
