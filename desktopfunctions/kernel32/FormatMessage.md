
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern uint FormatMessage(uint dwFlags, IntPtr lpSource,
   uint dwMessageId, uint dwLanguageId, [Out] StringBuilder lpBuffer,
   uint nSize, IntPtr Arguments);

// the version, the sample is built upon:
[DllImport("Kernel32.dll", SetLastError=true)]
static extern uint FormatMessage( uint dwFlags, IntPtr lpSource, 
   uint dwMessageId, uint dwLanguageId, ref IntPtr lpBuffer, 
   uint nSize, IntPtr pArguments);

// the parameters can also be passed as a string array:
[DllImport("Kernel32.dll", SetLastError=true)]
static extern uint FormatMessage( uint dwFlags, IntPtr lpSource, 
   uint dwMessageId, uint dwLanguageId, ref IntPtr lpBuffer, 
   uint nSize, string[] Arguments);

// simplified for usability
[DllImport("kernel32.dll")]
static extern int FormatMessage(
    FORMAT_MESSAGE dwFlags,
    IntPtr lpSource,
    int dwMessageId,
    uint dwLanguageId,
    out StringBuilder msgOut,
    int nSize,
    IntPtr Arguments
);
```

## C# Signature:
```cs
// see the sample code
[DllImport("kernel32.dll", SetLastError = true)]
static extern uint FormatMessage(uint dwFlags, IntPtr lpSource, uint dwMessageId, uint dwLanguageId, [Out] StringBuilder lpBuffer, uint nSize, string[] Arguments);
```

## VB.NET Signature:
```cs
<DllImport("Kernel32.dll", EntryPoint:="FormatMessageW", SetLastError:=True, CharSet:=CharSet.Unicode, CallingConvention:=CallingConvention.StdCall)> _
Public Shared Function FormatMessage(ByVal dwFlags As Integer, ByRef lpSource As IntPtr, ByVal dwMessageId As Integer, ByVal dwLanguageId As Integer, ByRef lpBuffer As [String], ByVal nSize As Integer, ByRef Arguments As IntPtr) As Integer
End Function
```

## VB.NET Signature:
```cs
<DllImport("Kernel32.dll", EntryPoint:="FormatMessageW", SetLastError:=True, CharSet:=CharSet.Unicode, CallingConvention:=CallingConvention.StdCall)> _
Public Shared Function FormatMessage(ByVal dwFlags As Integer, ByVal lpSource As IntPtr, ByVal dwMessageId As Integer, ByVal dwLanguageId As Integer, <MarshalAs(UnmanageType.LPWStr)> ByRef lpBuffer As String, ByVal nSize As Integer, ByVal Arguments As IntPtr) As Integer
End Function
```

## VB.NET Signature:
```cs
<DllImport("Kernel32.dll", EntryPoint:="FormatMessageW", SetLastError:=True, CharSet:=CharSet.Unicode, CallingConvention:=CallingConvention.StdCall)> _
Public Shared Function FormatMessage(ByVal dwFlags As Integer, ByVal lpSource As IntPtr, ByVal dwMessageId As Integer, ByVal dwLanguageId As Integer, ByRef lpBuffer As StringBuilder, ByVal nSize As Integer, ByVal Arguments As IntPtr) As Integer
End Function
```

## Sample Code:
```cs
enum FORMAT_MESSAGE : uint
{
    ALLOCATE_BUFFER = 0x00000100,
    IGNORE_INSERTS = 0x00000200,
    FROM_SYSTEM = 0x00001000,
    ARGUMENT_ARRAY = 0x00002000,
    FROM_HMODULE = 0x00000800,
    FROM_STRING = 0x00000400
}

[DllImport("kernel32.dll")]
static extern int FormatMessage(FORMAT_MESSAGE dwFlags, IntPtr lpSource, int dwMessageId, uint dwLanguageId, out StringBuilder msgOut, int nSize, IntPtr Arguments);

// 

public static int GetLastError()
{
    return (Marshal.GetLastWin32Error());
}

public static string GetLastErrorString()
{
    int lastError = GetLastError();
    if (0 == lastError) return ("");
    else
    {
       StringBuilder msgOut = new StringBuilder(256);
       int size = FormatMessage(FORMAT_MESSAGE.ALLOCATE_BUFFER | FORMAT_MESSAGE.FROM_SYSTEM | FORMAT_MESSAGE.IGNORE_INSERTS,
                     IntPtr.Zero, lastError, 0, out msgOut, msgOut.Capacity, IntPtr.Zero);
       return (msgOut.ToString().Trim());
    }
}
```

## Sample Code:
```cs
// from header files
    const uint FORMAT_MESSAGE_ALLOCATE_BUFFER = 0x00000100;
    const uint FORMAT_MESSAGE_IGNORE_INSERTS  = 0x00000200;
    const uint FORMAT_MESSAGE_FROM_SYSTEM    = 0x00001000;
    const uint FORMAT_MESSAGE_ARGUMENT_ARRAY = 0x00002000;
    const uint FORMAT_MESSAGE_FROM_HMODULE = 0x00000800;
    const uint FORMAT_MESSAGE_FROM_STRING = 0x00000400;

    int nLastError= Marshal.GetLastWin32Error();

    IntPtr lpMsgBuf= IntPtr.Zero;

    uint dwChars= FormatMessage( 
        FORMAT_MESSAGE_ALLOCATE_BUFFER | FORMAT_MESSAGE_FROM_SYSTEM | FORMAT_MESSAGE_IGNORE_INSERTS,
        IntPtr.Zero,
        (uint)nLastError,
        0, // Default language
        ref lpMsgBuf,
        0,
        IntPtr.Zero);
    if (dwChars==0)
    {
        // Handle the error.
        int le= Marshal.GetLastWin32Error();
        return null;
    }

    string sRet= Marshal.PtrToStringAnsi(lpMsgBuf);

    // Free the buffer.
    lpMsgBuf= LocalFree( lpMsgBuf );
    return sRet;

    // add for the forth signature
    try
    {
        StringBuilder msgBuilder = new StringBuilder(101);

        string formatExpression = "%1,%2%!";
        string[] formatArgs = new string[] { "Hello", "world" };

        IntPtr formatPtr = Marshal.StringToHGlobalAnsi(formatExpression);

        //must specify the FORMAT_MESSAGE_ARGUMENT_ARRAY flag when pass an array
        uint length = FormatMessage(FORMAT_MESSAGE_FROM_STRING | FORMAT_MESSAGE_ARGUMENT_ARRAY, formatPtr, 0, 0, msgBuilder, 101, formatArgs);

        if (length == 0)
        {
            FormatMessage(FORMAT_MESSAGE_FROM_SYSTEM, IntPtr.Zero, (uint)Marshal.GetLastWin32Error(), 0, msgBuilder, 101, null);

            Console.WriteLine("Error:" + msgBuilder.ToString());
        }
        else
        {
            Console.WriteLine("Format result:" + msgBuilder.ToString() + ", length:" + length.ToString());
        }
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.Message);
    }
```

## Sample Code:
```cs
<System.Runtime.InteropServices.DllImport("Kernel32.dll", EntryPoint:="FormatMessageW", SetLastError:=True, CharSet:=System.Runtime.InteropServices.CharSet.Unicode)>
    Public Shared Function FormatMessage(ByVal dwFlags As Integer, ByRef lpSource As IntPtr, ByVal dwMessageId As Integer, ByVal dwLanguageId As Integer, ByRef lpBuffer As IntPtr, ByVal nSize As Integer, ByRef Arguments As IntPtr) As Integer
    End Function

    <System.Runtime.InteropServices.DllImport("Kernel32.dll", SetLastError:=True)>
    Public Shared Function LocalFree(ByVal hMem As IntPtr) As IntPtr
    End Function

    Enum Format_Message
    FORMAT_MESSAGE_ALLOCATE_BUFFER = &H100 'The caller should use the LocalFree function to free the buffer when it is no longer needed
    FORMAT_MESSAGE_IGNORE_INSERTS = &H200
    FORMAT_MESSAGE_FROM_SYSTEM = &H1000
    'FORMAT_MESSAGE_ARGUMENT_ARRAY = &H2000
    'FORMAT_MESSAGE_FROM_HMODULE = &H800
    ''FORMAT_MESSAGE_FROM_STRING = &H400
    End Enum

    Private Sub Error_Message()
    'DllImport filed SetLastError must be set True
    'so Runtime.InteropServices.Marshal.GetLastWin32Error() returns a valid error
    Dim nLastError As Integer = Runtime.InteropServices.Marshal.GetLastWin32Error

    Dim lpMsgBuf As IntPtr = IntPtr.Zero

    Dim dwChars As Integer = FormatMessage(Format_Message.FORMAT_MESSAGE_ALLOCATE_BUFFER Or Format_Message.FORMAT_MESSAGE_FROM_SYSTEM Or Format_Message.FORMAT_MESSAGE_IGNORE_INSERTS,
    IntPtr.Zero, nLastError, 0, lpMsgBuf, 0, IntPtr.Zero)
    If dwChars = 0 Then
    Error_Message()
    Else
    Dim sRet As String = Runtime.InteropServices.Marshal.PtrToStringAuto(lpMsgBuf, dwChars)

    MessageBox.Show(sRet, "Error_Message()", MessageBoxButtons.OK, MessageBoxIcon.Error)
    End If

    'Format_Message.FORMAT_MESSAGE_ALLOCATE_BUFFER
    'The caller should use the LocalFree function to free the buffer when it is no longer needed
    If LocalFree(lpMsgBuf) <> 0 Then
    Error_Message()
    End If
    End Sub
```

## Sample Code:
```cs
[Flags]
    public enum FormatMessageFlags : int
    {
    FORMAT_MESSAGE_NONE = 0,
    FORMAT_MESSAGE_ALLOCATE_BUFFER = 0x00000100,
    FORMAT_MESSAGE_ARGUMENT_ARRAY = 0x00002000,
    FORMAT_MESSAGE_FROM_HMODULE = 0x00000800,
    FORMAT_MESSAGE_FROM_STRING = 0x00000400,
    FORMAT_MESSAGE_FROM_SYSTEM = 0x00001000,
    FORMAT_MESSAGE_IGNORE_INSERTS = 0x00000200,
    FORMAT_MESSAGE_MAX_WIDTH_MASK = 0x000000FF
    }

    public class Win32MessageProvider
    {

    private const int BUFF_SIZE = 1024;
    private static int[] _installedLcids;
    private int _lcid;

    static Win32MessageProvider()
    {
        CultureInfo[] cultures = CultureInfo.GetCultures(CultureTypes.InstalledWin32Cultures);
        _installedLcids = new int[cultures.Length];
        for (var i = 0; i < cultures.Length; i++)
        {
        _installedLcids[i] = cultures[i].LCID;
        }
    }

    public Win32MessageProvider()
    {
        _lcid = CultureInfo.CurrentCulture.LCID;
    }

    public Win32MessageProvider(int lcid)
    {
        if (_installedLcids.Contains(lcid))
        _lcid = lcid;
    }

    public Win32MessageProvider(CultureInfo culture)
    {
        if (_installedLcids.Contains(culture.LCID))
        _lcid = culture.LCID;
    }

    public string FormatMessage(uint messageId, FormatMessageFlags flags, string source, params string[] arguments)
    {
        if (string.IsNullOrEmpty(source))
        {
        flags &= ~FormatMessageFlags.FORMAT_MESSAGE_FROM_STRING;
        flags &= ~FormatMessageFlags.FORMAT_MESSAGE_FROM_HMODULE;
        }

        if (arguments.Length == 0)
        {
        flags &= ~FormatMessageFlags.FORMAT_MESSAGE_ARGUMENT_ARRAY;
        }

        StringBuilder buffer = new StringBuilder(BUFF_SIZE);
        IntPtr formatPtr = string.IsNullOrEmpty(source) ? IntPtr.Zero : Marshal.StringToHGlobalAnsi(source);
        int length = FormatMessage(flags, formatPtr, messageId, _lcid, buffer, BUFF_SIZE, arguments);
        string message = buffer.ToString(0, length);
        return message;
    }

    public string FormatMessage(uint messageId, params string[] arguments)
    {
        StringBuilder buffer = new StringBuilder(BUFF_SIZE);

        FormatMessageFlags flags = FormatMessageFlags.FORMAT_MESSAGE_FROM_SYSTEM;
        flags |= arguments.Length > 0
        ? FormatMessageFlags.FORMAT_MESSAGE_ARGUMENT_ARRAY
        : FormatMessageFlags.FORMAT_MESSAGE_IGNORE_INSERTS;

        int length = FormatMessage(flags, IntPtr.Zero, messageId, _lcid, buffer, BUFF_SIZE, arguments);
        string message = buffer.ToString(0, length);
        return message;
    }

    public string FormatMessage(uint messageId)
    {
        StringBuilder buffer = new StringBuilder(BUFF_SIZE);

        FormatMessageFlags flags = FormatMessageFlags.FORMAT_MESSAGE_FROM_SYSTEM |
                       FormatMessageFlags.FORMAT_MESSAGE_IGNORE_INSERTS;

        int length = FormatMessage(flags, IntPtr.Zero, messageId, _lcid, buffer, BUFF_SIZE, null);
        string message = buffer.ToString(0, length);
        return message;
    }

    public string FormatMessage(string moduleName, uint messageId, params string[] arguments)
    {
        StringBuilder buffer = new StringBuilder(BUFF_SIZE);
        IntPtr formatPtr = string.IsNullOrEmpty(message)
        ? IntPtr.Zero
        : GetModuleHandle(message);

        FormatMessageFlags flags = FormatMessageFlags.FORMAT_MESSAGE_FROM_HMODULE;
        flags |= arguments.Length > 0
        ? FormatMessageFlags.FORMAT_MESSAGE_ARGUMENT_ARRAY
        : FormatMessageFlags.FORMAT_MESSAGE_IGNORE_INSERTS;

        int length = FormatMessage(flags, modulePtr, messageId, _lcid, buffer, BUFF_SIZE, arguments);
        string message = buffer.ToString(0, length);
        return message;
    }

    public string FormatMessage(string message, params string[] arguments)
    {
        StringBuilder buffer = new StringBuilder(BUFF_SIZE);
        IntPtr formatPtr = string.IsNullOrEmpty(message)
        ? IntPtr.Zero
        : Marshal.StringToHGlobalAnsi(message);

        FormatMessageFlags flags = FormatMessageFlags.FORMAT_MESSAGE_FROM_STRING;
        flags |= arguments.Length > 0
        ? FormatMessageFlags.FORMAT_MESSAGE_ARGUMENT_ARRAY
        : FormatMessageFlags.FORMAT_MESSAGE_IGNORE_INSERTS;

        int length = FormatMessage(flags, formatPtr, 0, _lcid, buffer, BUFF_SIZE, arguments);
        message = buffer.ToString(0, length);
        return message;
    }

       [DllImport("kernel32.dll", SetLastError = true)]
    private static extern IntPtr GetModuleHandle(string lpModuleName);

       [DllImport("kernel32.dll", SetLastError = true)]
    [return: MarshalAs(UnmanagedType.I4)]
    private static extern int FormatMessage(
        [MarshalAs(UnmanagedType.I4)] FormatMessageFlags dwFlags, 
        IntPtr lpSource,
        uint dwMessageId,
        int dwLanguageId, 
        [Out] StringBuilder lpBuffer,
        int nSize, 
        string[] arguments);

    }
```

## Alternative Managed API:
```cs
string errorMessage = new Win32Exception(Marshal.GetLastWin32Error()).Message;
Console.WriteLine(errorMessage);
```
