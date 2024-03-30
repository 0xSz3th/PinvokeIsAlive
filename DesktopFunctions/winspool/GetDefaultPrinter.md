
## C# Signature:
```cs
[DllImport("winspool.drv", CharSet = CharSet.Auto, SetLastError = true)]
public static extern bool GetDefaultPrinter(StringBuilder pszBuffer, ref int pcchBuffer);
```

## VB Signature:
```cs
Declare Function GetDefaultPrinter Lib "winspool.drv" Alias "GetDefaultPrinterA" _ 
(ByVal pszBuffer As System.Text.StringBuilder, ByRef pcchBuffer As Int32) As Boolean
```

## Sample Code:
```cs
int pcchBuffer = 0;
    if (GetDefaultPrinter(null, ref pcchBuffer))
    {
    return null;
    }
    int lastWin32Error = Marshal.GetLastWin32Error();
    if (lastWin32Error == ERROR_INSUFFICIENT_BUFFER)
    {
    StringBuilder pszBuffer = new StringBuilder(pcchBuffer);
    if (GetDefaultPrinter(pszBuffer, ref pcchBuffer))
    {
        return pszBuffer.ToString();
    }
    lastWin32Error = Marshal.GetLastWin32Error();
    }
    if (lastWin32Error == ERROR_FILE_NOT_FOUND)
    {
    return null;
    }
    throw new Win32Exception(Marshal.GetLastWin32Error());
```

## Sample Code:
```cs
Private Shared Function _getDefaultPrinterName() As String
    Dim pszBuffer As System.Text.StringBuilder = New System.Text.StringBuilder(100)
    pszBuffer.Length = 100
    Dim pcchBuffer As Integer = CInt(pszBuffer.Length)
    Dim retVal As Boolean = GetDefaultPrinter(pszBuffer, pcchBuffer)
    Return pszBuffer.ToString.Trim    'StringBuilder manages the null-terminated string
    End Function
```
