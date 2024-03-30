
## C# Signature:
```cs
[DllImport("odbc32.dll", CharSet = CharSet.Unicode)]
static extern short SQLFreeHandle(ushort HandleType, IntPtr InputHandle);
```

## VB Signature:
```cs
Declare Function SQLFreeHandle Lib "odbc32.dll" (ByVal HandleType As Short, ByVal InputHandle As IntPtr) As Short
```

## Notes:
```cs
public const ushort SQL_HANDLE_ENV = 1;
public const ushort SQL_HANDLE_DBC = 2;
public const ushort SQL_HANDLE_STMT = 3;
public const ushort SQL_HANDLE_DESC = 4;
```
