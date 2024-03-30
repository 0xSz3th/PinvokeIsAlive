
## C# Signature:
```cs
[DllImport("odbc32.dll", CallingConvention=CallingConvention.Cdecl)]
static extern short SQLBindCol(HandleRef StatementHandle, short ColumnNumber, short 
TargetType, HandleRef TargetValue, int BufferLength, out IntPtr StrLen_or_Ind);
```

## VB Signature:
```cs
<DllImport("odbc32.dll", CallingConvention:=CallingConvention.Cdecl)> 
Shared Function SQLBindCol(ByVal StatementHandle As HandleRef, ByVal ColumnNumber As _
Short, ByVal TargetType As Short, ByVal TargetValue As HandleRef, ByVal BufferLength As _
IntPtr, <Out> ByRef StrLen_or_Ind As IntPtr) As Short
```

## C#
```cs
//****Show the user a list of all tables in a database****
            //Initialize pointers
            IntPtr environmentHandle = IntPtr.Zero;
            IntPtr dbcHandle = IntPtr.Zero;
            IntPtr stmtHandle = IntPtr.Zero;
            IntPtr temp = IntPtr.Zero;
            //Allocate some space to hold mapped table names
            IntPtr szTableName = Marshal.AllocHGlobal(256);
            short strLength = 0;
            //We will use a DSN in our connection string
            string connectionString = "DSN=SomeDSN; Uid=myun; Pwd=mypwd;";
            StringBuilder completedConnString = new StringBuilder(1024);

            //Allocate an environment handle to use
            SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, out environmentHandle);
            //Set the environment attribute SQL_ATTR_ODBC_VERSION to the latest version of ODBC driver
            SQLSetEnvAttr(environmentHandle.ToInt32(), SQL_ATTR_ODBC_VERSION, new IntPtr(SQL_OV_ODBC3), 0);
            //Allocate a database connection handle, using the environment handle we allocated earlier
            SQLAllocHandle(SQL_HANDLE_DBC, environmentHandle.ToInt32(), out dbcHandle);

            //Connect to the DB, the completed connection string will be passed back
            short retcode = SQLDriverConnect(dbcHandle, IntPtr.Zero, connectionString, 256, completedConnString, 1024, out strLength, SQL_DRIVER_COMPLETE);

            //Allocate a statment handle
            SQLAllocHandle(SQL_HANDLE_STMT, dbcHandle.ToInt32(), out stmtHandle);
            //Bind the 3rd column (Table Name) in the statement's return data to szTableName
            SQLBindCol(stmtHandle, 3, SQL_C_CHAR, szTableName, 256, out temp);

            //Get a list of the tables (no views) in the current DB
            SQLTables(stmtHandle, null, 0, null, 0, null, 0, "TABLE", -3);

            //Loop thru returned data
            StringBuilder str = new StringBuilder();
            while(SQLFetch(stmtHandle) != SQL_NO_DATA)
            {
                str.Append(Marshal.PtrToStringAnsi(szTableName));    
                str.Append("\r\n");
            }//end while

            //Free resources and disconnect
            SQLFreeStmt(stmtHandle, SQL_CLOSE);
            SQLFreeEnv(environmentHandle);
            SQLDisconnect(dbcHandle);
            SQLFreeHandle(SQL_HANDLE_DBC, dbcHandle);                        

            MessageBox.Show(str.ToString());
```
