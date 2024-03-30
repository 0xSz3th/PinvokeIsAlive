
## C# Signature:
```cs
[DllImport("odbccp32", CharSet=CharSet.Auto)]
public static extern SQL_RETURN_CODE    SQLInstallerError(int iError, ref SQL_INSTALLER_ERROR_CODE pfErrorCode, StringBuilder lpszErrorMsg, int cbErrorMsgMax, ref int pcbErrorMsg);
```

## VB Signature:
```cs
<DllImport("ODBCCP32.dll", CallingConvention:=CallingConvention.Winapi, CharSet:=CharSet.Auto, SetLastError:=True)> _
Public Shared Function SQLInstallerError(ByVal iError As Integer, ByRef pfErrorCode As Integer, ByVal lpszErrorMsg As StringBuilder, ByVal cbErrorMsgMax As Integer, ByRef pcbErrorMsg As Integer) As SQL_RETURN_CODE
End Function
```

## C# User-Defined Types:
```cs
public enum SQL_RETURN_CODE : short
{
    SQL_ERROR            = -1, 
    SQL_INVALID_HANDLE        = -2,
    SQL_SUCCESS        = 0,
    SQL_SUCCESS_WITH_INFO    = 1,
    SQL_STILL_EXECUTING    = 2,
    SQL_NEED_DATA        = 99,
    SQL_NO_DATA        = 100
}

public enum SQL_INSTALLER_ERROR_CODE : uint
{
     ODBC_ERROR_GENERAL_ERR = 1,
     ODBC_ERROR_INVALID_BUFF_LEN = 2,
     ODBC_ERROR_INVALID_HWND = 3,
     ODBC_ERROR_INVALID_STR = 4,
     ODBC_ERROR_INVALID_REQUEST_TYPE = 5,
     ODBC_ERROR_COMPONENT_NOT_FOUND = 6,
     ODBC_ERROR_INVALID_NAME = 7,
     ODBC_ERROR_INVALID_KEYWORD_VALUE = 8,
     ODBC_ERROR_INVALID_DSN = 9,
     ODBC_ERROR_INVALID_INF = 10,
     ODBC_ERROR_REQUEST_FAILED = 11,
     ODBC_ERROR_INVALID_PATH = 12,
     ODBC_ERROR_LOAD_LIB_FAILED = 13,
     ODBC_ERROR_INVALID_PARAM_SEQUENCE = 14,
     ODBC_ERROR_INVALID_LOG_FILE = 15,
     ODBC_ERROR_USER_CANCELED = 16,
     ODBC_ERROR_USAGE_UPDATE_FAILED = 17,
     ODBC_ERROR_CREATE_DSN_FAILED = 18,
     ODBC_ERROR_WRITING_SYSINFO_FAILED = 19,
     ODBC_ERROR_REMOVE_DSN_FAILED = 20,
     ODBC_ERROR_OUT_OF_MEM = 21,
     ODBC_ERROR_OUTPUT_STRING_TRUNCATED = 22,
     ODBC_ERROR_NOTRANINFO = 23
}
```

## VB.NET User-Defined Types:
```cs
Enum RequestFlags As Integer
  ODBC_ADD_DSN = 1
  ODBC_CONFIG_DSN = 2
  ODBC_REMOVE_DSN = 3
  ODBC_ADD_SYS_DSN = 4
  ODBC_CONFIG_SYS_DSN = 5
  ODBC_REMOVE_SYS_DSN = 6
  ODBC_REMOVE_DEFAULT_DSN = 7
End Enum
```

## Sample Code:
```cs
StringBuilder         errorMesg        = new StringBuilder( 512 ) ;
SQL_INSTALLER_ERROR_CODE  errorCode        = 0 ;
int               resizeErrorMesg    = 0 ;

//
// Get the error message
//
SQL_RETURN_CODE retCode = SQLInstallerError(1, ref errorCode, errorMesg, errorMesg.Capacity, ref resizeErrorMesg );
```

## VB.NET Sample Code
```cs
Dim errorMsg As New StringBuilder(512)
Dim errorCode As Integer = 0
Dim resizeErrorMesg As Integer = 0

' Get the error message
Dim retCode As SQL_RETURN_CODE = SQLInstallerError(1, errorCode, errorMsg, errorMsg.Capacity, resizeErrorMesg)
```
