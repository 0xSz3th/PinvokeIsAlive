
## C# Signature:
```cs
[DllImport("crypt32.dll", SetLastError = true)]
    public static extern IntPtr PFXImportCertStore(
        ref CRYPT_DATA_BLOB pPfx, 
        [MarshalAs(UnmanagedType.LPWStr)] String szPassword,
        uint dwFlags);
```

## VB Signature:
```cs
<DllImport("crypt32.dll", SetLastError:=True)> _
    Public Shared Function PFXImportCertStore( _
    ByRef pPfx As CRYPT_DATA_BLOB, _
    <MarshalAs(UnmanagedType.LPWStr)> ByVal szPassword As String, _
    ByVal dwFlags As Int32) As IntPtr
    End Function
```

## VB Signature:
```cs
Public Const CRYPT_EXPORTABLE As Int32 = &H1
    Public Const CRYPT_USER_PROTECTED As Int32 = &H2
    Public Const CRYPT_MACHINE_KEYSET As Int32 = &H20
    Public Const CRYPT_USER_KEYSET As Int32 = &H1000
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
    internal struct CRYPT_DATA_BLOB
    {
        public int cbData;
        public IntPtr pbData;
    }
```
