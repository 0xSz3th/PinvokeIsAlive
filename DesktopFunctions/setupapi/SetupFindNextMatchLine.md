
## C# Signature:
```cs
[DllImport("setupapi.dll", CharSet = CharSet.Auto, SetLastError = true)]
public static extern bool SetupFindNextMatchLine(ref INFCONTEXT ContextIn, [MarshalAs(UnmanagedType.LPTStr)] string Key, out INFCONTEXT ContextOut);
```

## VB Signature:
```cs
Public Declare Auto Function SetupFindNextMatchLine Lib "setupapi.dll" (ByRef ContextIn As INFCONTEXT, ByVal Key As String, ByRef ContextOut As INFCONTEXT) As Boolean
```

## Sample Code:
```cs
string infFile = <INF file full path>;
uint ErrorLine = 0;
IntPtr infHandle = SetupOpenInfFile(infFile, null, INF_STYLE_OLDNT | INF_STYLE_WIN4, out ErrorLine);
int iCode = Marshal.GetLastWin32Error();
if (infHandle.ToInt64() != INVALID_HANDLE_VALUE)
{
     Console.WriteLine("INF file was opened successfully.");
     INFCONTEXT Context = new INFCONTEXT();
     if (SetupFindFirstLine(infHandle, "Manufacturer", null, ref Context) == true)
     {
        Console.WriteLine("Manufacturers list (which match the specific key):");
        string manufacturerName = "";
        manufacturerName = manufacturerName.PadLeft(256, ' ');
        Int32 requiredSize = manufacturerName.Length;
        while(SetupFindNextMatchLine(ref Context, <key to search>, out Context) == true)
        {
            manufacturerName = manufacturerName.PadLeft(256, ' ');
            requiredSize = manufacturerName.Length;
            SetupGetStringField(ref Context, 1, manufacturerName, manufacturerName.Length, out requiredSize);
            manufacturerName = manufacturerName.Substring(0, requiredSize - 1);
            Console.WriteLine(manufacturerName);
        }
     }
     else
     {
        Console.WriteLine("Can't find [Manufacturer] section.");
     }
     SetupCloseInfFile(infHandle);
}
else
{
     Console.WriteLine("Failed to open INF file. Error code - {0}.", iCode);
     if (ErrorLine != 0)
     {
        Console.WriteLine("Failure line - {0}.", ErrorLine);
     }
}
```

## Sample Code:
```cs
Dim infFile As String = <INF file full path>
Dim ErrorLine As UInt32 = 0
Dim infHandle As IntPtr = SetupOpenInfFile(infFile, Nothing, INF_STYLE_OLDNT Or INF_STYLE_WIN4, ErrorLine)
Dim iCode As Integer = Marshal.GetLastWin32Error()
If infHandle.ToInt64() <> INVALID_HANDLE_VALUE Then
    Console.WriteLine("INF file was opened successfully.")
    Dim Context As INFCONTEXT = New INFCONTEXT()
    If SetupFindFirstLine(infHandle, "Manufacturer", Nothing, Context) = True Then
        Console.WriteLine("Manufacturers list (which match the specific key):")
        Dim manufacturerName As String = ""
        manufacturerName = manufacturerName.PadLeft(256, " "c)
        Dim requiredSize As Int32 = manufacturerName.Length
        While SetupFindNextMatchLine(Context, <key to search>, Context) = True
            SetupGetStringField(Context, 1, manufacturerName, manufacturerName.Length, requiredSize)
            manufacturerName = manufacturerName.Substring(0, requiredSize - 1)
            Console.WriteLine(manufacturerName)
        End While
    Else
        Console.WriteLine("Can't find [Manufacturer] section.")
    End If
    SetupCloseInfFile(infHandle)
Else
    Console.WriteLine("Failed to open INF file. Error code - {0}.", iCode)
    If ErrorLine <> 0 Then
        Console.WriteLine("Failure line - {0}.", ErrorLine)
    End If
End If
```
