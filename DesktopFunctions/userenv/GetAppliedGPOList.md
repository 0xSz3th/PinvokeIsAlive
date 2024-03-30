
## C# Signature:
```cs
[DllImport("userenv.dll", SetLastError=true)]
extern static int GetAppliedGPOList(
        int dwFlags,
        string pMachineName,
        IntPtr pSidUser,
        IntPtr pGuidExtension,
        ref IntPtr ppGPOList);
```

## VB Signature:
```cs
Declare Function GetAppliedGPOList Lib "userenv.dll" (TODO) As TODO
```

## Win32 API:
```cs
__in      DWORD dwFlags,
  __in      LPCTSTR pMachineName,
  __in      PSID pSidUser,
  __in      GUID* pGuidExtension,
  __out     PGROUP_POLICY_OBJECT* ppGPOList
```
