
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct CERT_CONTEXT
{
    public uint    dwCertEncodingType;
    [MarshalAs(UnmanagedType.LPArray, SizeParamIndex=2)] 
     public byte[]    pbCertEncoded;
    public uint    cbCertEncoded;
    public IntPtr    pCertInfo;
    public IntPtr    hCertStore;
}
```

## VB Definition:
```cs
Structure CERT_CONTEXT 
   Public TODO
End Structure
```
