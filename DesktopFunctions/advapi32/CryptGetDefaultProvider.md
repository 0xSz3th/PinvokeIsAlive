
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError=true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool CryptGetDefaultProvider(
    UInt32 dwProvType,
    IntPtr pdwReserved,
    UInt32 dwFlags,
    StringBuilder pszProvName,
    ref IntPtr ProvName
);
```

## VB Signature:
```cs
Declare Function CryptGetDefaultProvider Lib "advapi32.dll" (TODO) As TODO
```

## User-Defined Types:
```cs
// Possible values for dwFlags
const UInt32 CRYPT_USER_DEFAULT = 0x00000002;
const UInt32 CRYPT_MACHINE_DEFAULT = 0x00000001;
```

## Sample Code:
```cs
StringBuilder providerName = new StringBuilder(255);
IntPtr providerNameLen = new IntPtr(255);

if (CryptGetDefaultProvider(
    PROV_RSA_FULL,
    IntPtr.Zero,
    CRYPT_USER_DEFAULT,
    providerName,
    ref providerNameLen))
{
    MessageBox.Show(String.Format("The default provider is {0}", providerName.ToString()));
}
else
{
    MessageBox.Show("Unable to get the default provider");
}
```
