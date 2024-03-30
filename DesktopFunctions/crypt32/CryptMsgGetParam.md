
## C# Signature:
```cs
[DllImport("crypt32.dll", SetLastError=true)]
public static extern bool CryptMsgGetParam(
     IntPtr hCryptMsg,
     uint dwParamType,
     uint dwIndex,
     IntPtr pvData,
     ref uint pcbData
);
```
