
## C# Signature:
```cs
[DllImport ( "kernel32.dll" ,
           SetLastError = true ,
           CharSet = CharSet.Auto )]
static extern uint SearchPath ( string lpPath ,
                 string lpFileName ,
                 string lpExtension ,
                 int nBufferLength ,
                 [MarshalAs ( UnmanagedType.LPTStr )]
                 StringBuilder lpBuffer ,
                 out IntPtr lpFilePart );
```

## Sample Code:
```cs
[DllImport ( "kernel32.dll" ,
           SetLastError = true ,
           CharSet = CharSet.Auto )]
public static extern uint SearchPath ( string lpPath ,
                    string lpFileName ,
                    string lpExtension ,
                    int nBufferLength ,
                    [MarshalAs ( UnmanagedType.LPTStr )]
                    StringBuilder lpBuffer ,
                    out IntPtr lpFilePart );

static void Main ( string [] args )
{
    StringBuilder sb = new StringBuilder ( 260 );
    IntPtr ptr = new IntPtr ( );

    SearchPath ( null ,
        "NOTEPAD.EXE" ,
         null ,
         sb.Capacity ,
         sb ,
         out ptr );

   Console.WriteLine ( sb.ToString ( ) );
}
```
