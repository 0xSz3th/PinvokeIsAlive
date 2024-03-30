
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool EnumDesktops(IntPtr hwinsta, EnumDesktopsDelegate
   lpEnumFunc, IntPtr lParam);
```

## VB.NET Signature
```cs
<Runtime.InteropServices.DllImport("user32.dll")>
Private Function EnumDesktops(ByVal hwinsta As IntPtr, ByVal lpEnumFunc As EnumDesktopsDelegate, ByVal lParam As IntPtr) As Boolean
End Function
```

## Sample Code:
```cs
private delegate bool EnumDesktopsDelegate(string desktop, IntPtr lParam);

    [DllImport("user32.dll")]
    static extern bool EnumDesktops(IntPtr hwinsta, EnumDesktopsDelegate
                        lpEnumFunc, IntPtr lParam);

    private static bool _enumDesktopCallback( string desktop, IntPtr lParam )
    {
        GCHandle gch       = GCHandle.FromIntPtr( lParam );
        IList<string> list = gch.Target as List<string>;

        if ( null == list ) {
        return (false);
        }

        list.Add( desktop );

        return (true);
    }

    int _doEnumDesktops()
    {
        IList<string> list       = new List<string>();
        GCHandle gch         = GCHandle.Alloc( list );
        EnumDesktopsDelegate childProc = _enumDesktopCallback;

        if (!EnumDesktops(IntPtr.Zero, childProc, GCHandle.ToIntPtr( gch ) ))
        {
        int e = Marshal.GetLastWin32Error();
        WriteLine( "EnumDesktops errno={0}",  e );
        return 1;
        }

        foreach ( string a in list ) {
        Console.WriteLine( a );
        }

        return 0;
    }
```
