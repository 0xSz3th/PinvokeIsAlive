
## C# Signature:
```cs
[DllImport("advapi32.dll", CharSet=CharSet.Auto, SetLastError=true)]
public extern static bool DuplicateTokenEx(
    IntPtr hExistingToken,
    uint dwDesiredAccess,
    ref SECURITY_ATTRIBUTES lpTokenAttributes,
    SECURITY_IMPERSONATION_LEVEL ImpersonationLevel,
    TOKEN_TYPE TokenType,
    out IntPtr phNewToken );
```

## C# Signature
```cs
public extern static bool DuplicateTokenEx(
        IntPtr hExistingToken,
        uint dwDesiredAccess,
        IntPtr lpTokenAttributes,
        uint ImpersonationLevel,
        uint TokenType,
        out IntPtr phNewToken);
```

## VB Signature:
```cs
Declare Auto Function DuplicateTokenEx Lib "advapi32.dll" ( _
    ByVal ExistingTokenHandle As IntPtr, _
    ByVal dwDesiredAccess As UInt32, _
    ByRef lpThreadAttributes As SECURITY_ATTRIBUTES, _
    ByVal ImpersonationLevel As Integer, _
    ByVal TokenType As Integer, _
    ByRef DuplicateTokenHandle As System.IntPtr) As Boolean

<DllImport("advapi32.dll", CharSet:=CharSet.Auto, SetLastError:=True)>
    Public Shared Function DuplicateTokenEx(hExistingToken As IntPtr, dwDesiredAccess As UInteger, lpTokenAttributes As IntPtr, ImpersonationLevel As SECURITY_IMPERSONATION_LEVEL, TokenType As TOKEN_TYPE, ByRef phNewToken As IntPtr) As Boolean
    End Function
```

## Tips & Tricks:
```cs
Const GRANTED_ALL As String = "10000000"

    ret = DuplicateTokenEx(Token, UInt32.Parse(GRANTED_ALL, System.Globalization.NumberStyles.HexNumber), sa, SecurityImpersonation, TokenType, DupedToken)
```
