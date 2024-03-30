
## C# Signature:
```cs
[DllImport("CRYPT32.DLL", EntryPoint = "CryptQueryObject", CharSet = CharSet.Auto, SetLastError = true)]
    public static extern Boolean CryptQueryObject(
        Int32 dwObjectType,
        [MarshalAs(UnmanagedType.LPWStr)]String pvObject,
        uint dwExpectedContentTypeFlags,
        uint dwExpectedFormatTypeFlags,
        uint dwFlags,
        ref uint pdwMsgAndCertEncodingType,
        ref uint pdwContentType,
        ref uint pdwFormatType,
        ref IntPtr phCertStore,
        ref IntPtr phMsg,
        ref IntPtr ppvContext
    );
```

## VB Signature:
```cs
Declare Function CryptQueryObject Lib "crypt32.dll" (TODO) As TODO
```
