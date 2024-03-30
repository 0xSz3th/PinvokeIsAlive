
## C# Signature:
```cs
[DllImport("odbc32.dll", SetLastError=true)]
static extern short SQLSetEnvAttr ( 
    IntPtr envHandle, 
    int attribute, 
    IntPtr attrValue, 
    int stringLength );
```

## Alternate C# Signature:
```cs
static extern short SQLSetEnvAttr ( 
    IntPtr envHandle, 
    int attribute, 
    int    attrValue, 
    int stringLength );
```

## VB Signature:
```cs
Private Declare Auto Function SQLSetEnvAttr Lib "odbc32.dll" ( _
    ByVal henv As IntPtr, _
    ByVal attribute As Integer, _
    ByVal valuePtr As IntPtr, _
    ByVal strLength As Integer ) As Short
```
