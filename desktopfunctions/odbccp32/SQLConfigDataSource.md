
## C# Signature:
```cs
[DllImport("ODBCCP32.DLL",CharSet=CharSet.Unicode, SetLastError=true)]
static extern bool SQLConfigDataSourceW(IntPtr hwndParent , RequestFlags fRequest, string lpszDriver, string lpszAttributes);
```

## VB Signature:
```cs
<DllImport("ODBCCP32.dll",CallingConvention:=CallingConvention.WinAPI,CharSet:=CharSet.Unicode,SetLastError:=True)> _
Public Shared Function SQLConfigDataSourceW(ByVal hwndParent As IntPtr, ByVal fRequest As UShort, ByVal lpszDriver As String, ByVal lpszAttributes As String) As Boolean
```

## User-Defined Types:
```cs
ODBC_ADD_DSN = 1,
    ODBC_CONFIG_DSN = 2,
    ODBC_REMOVE_DSN = 3,
    ODBC_ADD_SYS_DSN = 4,
    ODBC_CONFIG_SYS_DSN = 5,
    ODBC_REMOVE_SYS_DSN = 6,
    ODBC_REMOVE_DEFAULT_DSN = 7
```

## Tips & Tricks:
```cs
EG:
String.Format("CREATE_DBV4=\"{0}\" General\0", FileName);
```

## Sample Code:
```cs
using System;
using System.Runtime.InteropServices;

namespace PInvoke
{
    /// <summary>
    /// JetSQL is the "code name" for the SQL engine behind Microsoft Access. It's
    /// actually built into Windows, Microsoft Access is just a front end interface
    /// for the Jet Engine.
    /// </summary>
    public static class JetSql
    {
        // The driver to use for the datasource.
        private const string MS_ACCESS_DRIVER = "Microsoft Access Driver (*.mdb)";

        private enum RequestFlags : ushort
        {
            ODBC_ADD_DSN = 1,            // Add a new user data source.
            ODBC_CONFIG_DSN = 2,         // Configure (modify) an existing user data source.
            ODBC_REMOVE_DSN = 3,         // Remove an existing user data source.
            ODBC_ADD_SYS_DSN = 4,        // Add a new system data source.
            ODBC_CONFIG_SYS_DSN = 5,         // Modify an existing system data source.
            ODBC_REMOVE_SYS_DSN = 6,         // Remove an existing system data source.
            ODBC_REMOVE_DEFAULT_DSN = 7      // Remove the default data source specification section from the system information.
        }

        /// <summary>
        /// A method to dynamically add DSN-names to the system. This method also
        /// aids with the creation, and subsequent manipulation, of Microsoft
        /// Access database files.
        /// <see cref="http://msdn.microsoft.com/library/default.asp?url=/library/en-us/odbc/htm/odbcsqlconfigdatasource.asp"/>
        /// </summary>
        /// </summary>
        /// <param name="hwndParent">Parent window handle. The function will not display
        /// any dialog boxes if the handle is null.</param>
        /// <param name="fRequest">One of the OdbcConstant enum values to specify the
        /// type of the request (RequestFlags.ODBC_ADD_DSN to create an MDB).</param>
        /// <param name="lpszDriver">Driver description (usually the name of the
        /// associated DBMS) presented to users instead of the physical driver name.</param>
        /// <param name="lpszAttributes">List of attributes in the form of keyword-value
        /// pairs. For more information, see
        /// <see cref="http://msdn.microsoft.com/library/en-us/odbc/htm/odbcconfigdsn.asp">ConfigDSN</see>
        /// in Chapter 22: Setup DLL Function Reference.</param>
        /// <returns>The function returns TRUE if it is successful, FALSE if it fails.
        /// If no entry exists in the system information when this function is called,
        /// the function returns FALSE.</returns>
        [DllImport("ODBCCP32.DLL", CharSet=CharSet.Unicode, SetLastError=true)]
        private static extern bool SQLConfigDataSourceW(UInt32 hwndParent , RequestFlags fRequest, string lpszDriver, string lpszAttributes);

        /// <summary>
        /// Compacts an MS Access database.
        /// </summary>
        /// <param name="DatabasePath">The path of the database to be compacted.</param>
        /// <returns>A boolean value indicating success.</returns>
        public static bool CompactDatabase(string DatabasePath)
        {
            string attributes = String.Format("COMPACT_DB=\"{0}\" \"{0}\" General\0", DatabasePath);
            return SQLConfigDataSourceW(NULL_HWND, RequestFlags.ODBC_ADD_DSN, MS_ACCESS_DRIVER, attributes);
        }

        /// <summary>
        /// Creates an MS Access database.
        /// </summary>
        /// <param name="DatabasePath">The path of the database to be created.</param>
        /// <returns>A boolean value indicating success.</returns>
        public static bool CreateDatabase(string DatabasePath)
        {
            string attributes = String.Format("CREATE_DB=\"{0}\" General\0", DatabasePath);
            return SQLConfigDataSourceW(IntPtr.Zero, RequestFlags.ODBC_ADD_DSN, MS_ACCESS_DRIVER, attributes);
        }

        /// <summary>
        /// Repairs an MS Access Database.
        /// </summary>
        /// <param name="DatabasePath">The path of the database to be repaired.</param>
        /// <returns>A boolean value indicating success.</returns>
        public static bool RepairDatabase(string DatabasePath)
        {
            string attributes = String.Format("REPAIR_DB=\"{0}\" General\0", DatabasePath);
            return SQLConfigDataSourceW(IntPtr.Zero, RequestFlags.ODBC_ADD_DSN, MS_ACCESS_DRIVER, attributes);
        }
    }
}
```

## Sample Code:
```cs
ODBC_ADD_DSN = 1,
    ODBC_CONFIG_DSN = 2,
    ODBC_REMOVE_DSN = 3,
    ODBC_ADD_SYS_DSN = 4,
    ODBC_CONFIG_SYS_DSN = 5,
    ODBC_REMOVE_SYS_DSN = 6,
    ODBC_REMOVE_DEFAULT_DSN = 7
```

## Sample Code:
```cs
<DllImport("ODBCCP32.dll",CallingConvention:=CallingConvention.WinAPI,CharSet:=CharSet.Unicode,SetLastError:=True)> _
Private Shared Function SQLConfigDataSourceW(ByVal hwndParent As IntPtr, ByVal fRequest As RequestFlags, ByVal lpszDriver As String, ByVal lpszAttributes As String) As Boolean

Private Function CreateSystemDSN() As Boolean
    Dim vAttributes As String = "DSN=My DSN Name" & Convert.ToChar(0)
    vAttributes &= "Description=My DSN Description" & Convert.ToChar(0)
    vAttributes &= "Trusted_Connection=Yes" & Convert.ToChar(0)
    vAttributes &= "Server=SQLSERVERINSTANCE" & Convert.ToChar(0)
    vAttributes &= "Database=MyDatabaseName" & Convert.ToChar(0)

    If SQLConfigDataSourceW(IntPtr.Zero, RequestFlags.ODBC_ADD_SYS_DSN, "SQL Server", vAttributes) = 0 Then
        Messagebox.Show("Failed to create ODBC data source!!")
        Return False
    End If
    Return True
End Function
```
