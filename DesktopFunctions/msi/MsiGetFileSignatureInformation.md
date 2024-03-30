
## C# Signature:
```cs
[Flags]
  public enum MSISIGINFO : uint
  {
      None = 0,
      MSI_INVALID_HASH_IS_FATAL = 1
  }

  public enum HRESULT
  {
      S_OK = unchecked(0x00000000),
      S_FALSE = unchecked(0x00000001),
      E_FAIL = unchecked((int)0x80004005),
      E_INVALIDARG = unchecked((int)0x80070057),
      E_MOREDATA = unchecked((int)0x800700EA),
      E_OUTOFMEMORY = unchecked((int)0x8007000E),
      ERROR_FUNCTION_FAILED = unchecked((int)0x8007065B),
      TRUST_E_NOSIGNATURE = unchecked((int)0x800B0100),
      TRUST_E_BAD_DIGEST = unchecked((int)0x80096010),
      CERT_E_REVOKED = unchecked((int)0x800B010C),
      TRUST_E_SUBJECT_NOT_TRUSTED = unchecked((int)0x800B0004),
      TRUST_E_PROVIDER_UNKNOWN = unchecked((int)0x800B0001),
      TRUST_E_ACTION_UNKNOWN = unchecked((int)0x800B0002),
      TRUST_E_SUBJECT_FORM_UNKNOWN = unchecked((int)0x800B0003),
  }

  [StructLayout(LayoutKind.Sequential)]
  public struct CERT_CONTEXT
  {
      public CertEncodingType dwCertEncodingType;
      public IntPtr pbCertEncoded;
      public uint cbCertEncoded;
      public IntPtr pCertInfo;
      public IntPtr hCertStore;
  }

  [DllImport("msi.dll", CharSet = CharSet.Unicode)]
  [DefaultDllImportSearchPaths(DllImportSearchPath.System32)]
  public static extern HRESULT MsiGetFileSignatureInformation(
      [In] string szSignedObjectPath,
      [In] MSISIGINFO dwFlags,
      [In, Out] ref IntPtr ppcCertContext,
      [Out] byte[] pbHashData,
      [In, Out] ref int pcbHashData);
```

## Sample Code:
```cs
CERT_CONTEXT certContext = default;
  try
  {
      // - First call gets the hash data buffer size.
      // - Second call gets the hash data for real.
      byte[] pbHashData = Array.Empty<byte>();
      int pcbHashData = 0;
      HRESULT hresult = HRESULT.E_MOREDATA;
      for (int i = 0; i < 2 && hresult == HRESULT.E_MOREDATA; i++)
      {
          hresult = MsiGetFileSignatureInformation(
          msiFilePath,
          MSISIGINFO.MSI_INVALID_HASH_IS_FATAL,
          ref pCertContext,
          pbHashData,
          ref pcbHashData);

          if (hresult == HRESULT.E_MOREDATA)
          {
              // pbHashData is ready to use now.
              pbHashData = new byte[pcbHashData];
          }
      }

      // Copy PCCERT_CONTEXT from the unmanaged space to CERT_CONTEXT in managed space.
      // certContext is ready to use now.
      certContext =
          pCertContext == IntPtr.Zero
          ? default
          : Marshal.PtrToStructure<CERT_CONTEXT>(pCertContext);
  }
  finally
  {
      // The PCCERT_CONTEXT returned by MsiGetFileSignatureInformation must be
      // freed with CertFreeCertificateContext.
      if (pCertContext != IntPtr.Zero)
      {
          CertFreeCertificateContext(pCertContext);
      }
  }
```
