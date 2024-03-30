
## C# Signature:
```cs
[DllImport("urlmon.dll", CharSet=CharSet.Ansi)] 
private static extern int UrlMkGetSessionOption(int dwOption, StringBuilder pBuffer, int dwBufferLength, out int pdwBufferLength, int dwReserved);
```

## VB Signature:
```cs
<DllImport("urlmon.dll", CharSet:=CharSet.Ansi)> _
Private Shared Function UrlMkGetSessionOption( _
     ByVal dwOption As Integer, _
     ByVal pBuffer As StringBuilder, _
     ByVal dwBufferLength As Integer, _
     ByRef pdwBufferLength As Integer, _
     ByVal dwReserved As Integer _
     ) As Integer
End Function
```

## User-Defined Types:
```cs
Private Const URLMON_OPTION_USERAGENT As Integer = &H10000001
Private Const URLMON_OPTION_USERAGENT_REFRESH As Integer = &H10000002
Private Const URLMON_OPTION_URL_ENCODING As Integer = &H10000004
```

## Sample Code:
```cs
Dim buffer As New StringBuilder(255)
Dim returnLength As Integer
Dim ret As Integer = UrlMkGetSessionOption(URLMON_OPTION_USERAGENT, buffer, buffer.Capacity, returnLength, 0)
```
