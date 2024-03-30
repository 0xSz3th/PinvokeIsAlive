
## C# Signature:
```cs
[DllImport("odbc32.dll")]
static extern short SQLAllocEnv(out IntPtr EnvironmentHandle);
```

## User-Defined Types:
```cs
//return values
    const short SQL_SUCCESS             =   0;
    const short SQL_SUCCESS_WITH_INFO   =   1;    
    const short SQL_STILL_EXECUTING     =   2;
    const short SQL_NEED_DATA           =  99;
    const short SQL_NO_DATA             = 100;
    const short SQL_ERROR               = (-1);
    const short SQL_INVALID_HANDLE      = (-2);
```

## Sample Code:
```cs
IntPtr environmentHandle = IntPtr.Zero;
    short  rc = SQLAllocEnv(out environmentHandle);
    if (rc != SQL_SUCCESS && rc != SQL_SUCCESS_WITH_INFO)
    {
        throw new Exception("Failed to allocate environment handle.");
    }
```
