
## C# Signature:
```cs
[DllImport("odbccp32.dll", SetLastError=true)]
static extern int SQLGetPrivateProfileString(string lpszSection, string lpszEntry, string lpszDefault, [Out] char[] retBuffer, int cbRetBuffer, string lpszFileName);
```

## VB Signature:
```cs
Declare Function SQLGetPrivateProfileString Lib "odbccp32.dll" (TODO) As TODO
```

## Sample Code:
```cs
void UpdateDSN(string dataSourceName, string connStr)
{
    char[] value = new char[8192];

    // Try to retrieve the driver for the data source
    SQLSetConfigMode(ConfigMode.ODBC_SYSTEM_DSN);
    SQLGetPrivateProfileString(dataSourceName, "Driver", "", value, value.Length, "odbc.ini");

    // Set our configuration mode
    RequestFlags configMode = value[0] == '\0' ? RequestFlags.ODBC_ADD_SYS_DSN : RequestFlags.ODBC_CONFIG_SYS_DSN;

    // Connection string for SQLConfigDataSource must be null-
    // character delimited and double null-terminated
    string s = connStr.Replace(';', '\0');
    s += '\0';

    // Persist the data source
    SQLConfigDataSourceW(0, configMode, MY_DRIVER_NAME_STRING, s);
}
```
