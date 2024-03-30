
## C# Signature:
```cs
/// <summary>
/// SQLDataSources returns information about a data source. This function is implemented solely by the Driver Manager.
/// </summary>
/// <param name="EnvironmentHandle">[Input] Environment handle.</param>
/// <param name="Direction">[Input] Determines which data source the Driver Manager returns information on.</param>
/// <param name="ServerName">[Output] Pointer to a buffer in which to return the data source name.</param>
/// <param name="BufferLength1">[Input] Length of the *ServerName buffer, in characters; this does not need to be longer than SQL_MAX_DSN_LENGTH plus the null-termination character.</param>
/// <param name="NameLength1Ptr">[Output] Pointer to a buffer in which to return the total number of bytes (excluding the null-termination byte) 
/// available to return in *ServerName. If the number of bytes available to return is greater than or equal to BufferLength1, the data 
/// source name in *ServerName is truncated to BufferLength1 minus the length of a null-termination character. </param>
/// <param name="Description">[Output] Pointer to a buffer in which to return the description of the driver associated with the data source. 
/// For example, dBASE or SQL Server.</param>
/// <param name="BufferLength2">[Input] Length in characters of the *Description buffer.</param>
/// <param name="NameLength2Ptr">[Output] Pointer to a buffer in which to return the total number of bytes (excluding the null-termination 
/// byte) available to return in *Description. If the number of bytes available to return is greater than or equal to BufferLength2, 
/// the driver description in *Description is truncated to BufferLength2 minus the length of a null-termination character.</param>
/// <returns>SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR, or SQL_INVALID_HANDLE.</returns>
[DllImport("odbc32.dll", CharSet=CharSet.Ansi))]
static extern short SQLDataSources(IntPtr EnvironmentHandle, short Direction, 
    StringBuilder ServerName, short BufferLength1, ref short NameLength1Ptr, 
    StringBuilder Description, short BufferLength2, ref short NameLength2Ptr);
```

## VB Signature:
```cs
Declare Function SQLDataSources Lib "odbc32.dll" (ByVal EnvironmentHandle As Integer, ByVal Direction As Short, _
    ByVal ServerName As String, ByVal BufferLength1 As Short, ByRef NameLength1Ptr As Short, _
    ByVal Description As String, ByVal BufferLength2 As Short, ByRef NameLength2Ptr As Short) As Short
```

## Sample Code:
```cs
public const ushort SQL_HANDLE_ENV = 1;
public const short SQL_SUCCESS = 0;
public const short SQL_SUCCESS_WITH_INFO = 1;
public const short SQL_NO_DATA = 100;
public const int SQL_ATTR_ODBC_VERSION = 200;
public const int SQL_OV_ODBC3 = 3;
public const short SQL_FETCH_NEXT = 1;
public const short SQL_FETCH_FIRST = 2;
public const int MAX_DSN_LENGTH = 32;

/// <summary>
/// Obtains all the ODBC DSNs installed on the system and returns them in a List<string> object.
/// </summary>
public static List<string> GetOdbcDataSources()
{
    IntPtr sql_env_handle = IntPtr.Zero;
    short rc = 0;
    StringBuilder dsn_name = new StringBuilder(MAX_DSN_LENGTH);
    StringBuilder desc_name = new StringBuilder(128);
    short dsn_name_len = 0,desc_len = 0;
    List<String> rv = new List<String>();

    try
    {
    rc = SQLAllocHandle(SQL_HANDLE_ENV, 0, out sql_env_handle);
    if ((rc != SQL_SUCCESS) && (rc != SQL_SUCCESS_WITH_INFO))
        throw new Exception("Could not allocate ODBC Environment handle");
    rc = SQLSetEnvAttr(sql_env_handle, SQL_ATTR_ODBC_VERSION, (IntPtr)SQL_OV_ODBC3, 0);
    if ((rc != SQL_SUCCESS) && (rc != SQL_SUCCESS_WITH_INFO))
        throw new Exception("Could not setup ODBC Environment handle");
    rc = SQLDataSources(sql_env_handle, SQL_FETCH_FIRST, dsn_name, (short)dsn_name.Capacity, ref dsn_name_len, desc_name, (short) desc_name.Capacity, ref desc_len);
    if ((rc != SQL_SUCCESS) && (rc != SQL_SUCCESS_WITH_INFO) && (rc != SQL_NO_DATA))
        throw new Exception("Error getting ODBC Data Sources");
    while ((rc == SQL_SUCCESS) || (rc == SQL_SUCCESS_WITH_INFO))
    {
        rv.Add(dsn_name.ToString());
        rc = SQLDataSources(sql_env_handle, SQL_FETCH_NEXT, dsn_name, (short)dsn_name.Capacity, ref dsn_name_len, desc_name, (short)desc_name.Capacity, ref desc_len);
        if ((rc != SQL_SUCCESS) && (rc != SQL_SUCCESS_WITH_INFO) && (rc != SQL_NO_DATA))
        throw new Exception("Error getting ODBC Data Sources");
    }
    }
    finally
    {
    if (sql_env_handle != IntPtr.Zero)
    {
        rc = SQLFreeHandle(SQL_HANDLE_ENV, sql_env_handle);
        if ((rc != SQL_SUCCESS) && (rc != SQL_SUCCESS_WITH_INFO))
        throw new Exception("Could not free ODBC Environment handle");
    }
    }
    return rv;
}
```

## Sample Code:
```cs
Private Sub OnGetODBCConnectionNames(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles cmbExpSID.DropDown, cmbImpSid.DropDown
    Dim c As ComboBox = sender

    Dim hEnv As IntPtr
    c.Items.Clear()

    Try
        SQLAllocEnv(hEnv)

        If (hEnv) Then
        Dim iNameLen As Short = 0
        Dim iNameLen2 As Short = 0
        Dim nResult As Short = 0
        Dim cDSNBuf(64) As Char
        Dim cDescBuf(64) As Char
        Dim sDSN As String = New String(cDSNBuf)
        Dim sDesc As String = New String(cDescBuf)

        Dim Dir As SQLVals = SQLVals.SQL_FETCH_NEXT

        Dim i As Integer = 0
        nResult = SQLDataSources(hEnv, Dir, sDSN, 64, iNameLen, sDesc, 64, iNameLen2)
        While ((nResult <> SQLVals.SQL_NO_DATA_FOUND) And (nResult <> SQLVals.SQL_ERROR))

            c.Items.Add(Trim(sDSN))
            nResult = SQLDataSources(hEnv, Dir, sDSN, 64, iNameLen, sDesc, 64, iNameLen2)
            i = i + 1
        End While
```

## Sample Code:
```cs
End If

    Finally
        If (hEnv) Then
        SQLFreeEnv(hEnv)
        End If
    End Try

    End Sub
```

## Alternative Managed API:
```cs
Dim strKeyNames() As String
        Dim intKeyValues As Integer
        Dim intCount As Integer
        Dim key As Microsoft.Win32.RegistryKey

        key = Microsoft.Win32.Registry.LocalMachine.OpenSubKey("software\odbc\odbc.ini\odbc data sources")
        strKeyNames = key.GetValueNames() 'Get an array of the value names
        intKeyValues = key.ValueCount() 'Get the number of values
        For intCount = 0 To intKeyValues - 1
        If key.GetValue(strKeyNames(intCount)) = "SQL Server" Then 'only add DSNs that are for SQL Server
            cboDSN.Items.Add(strKeyNames(intCount))
        End If
        Next
```
