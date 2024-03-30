
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError=true)]
static extern bool CreateWellKnownSid(
    WELL_KNOWN_SID_TYPE WellKnownSidType,
    IntPtr DomainSid,
    IntPtr pSid,
    ref uint cbSid);
```

## VB.Net Signature:
```cs
Private Declare Function CreateWellKnownSid Lib "advapi32.dll" ( _
    ByVal WellKnownSidType As Integer, _
    ByVal DomainSid As IntPtr, _
    ByVal pSID As IntPtr, _
    ByRef cbSid As Integer _
    ) As Boolean
```

## Sample Code:
```cs
string GetWellKnownSID(WELL_KNOWN_SID_TYPE wellKnownSidType)
  {
      IntPtr domainSid = IntPtr.Zero;
      IntPtr pSid = IntPtr.Zero;
      uint cbSid = 0;
      string sidString = string.Empty;

      NativeMethods.CreateWellKnownSid(wellKnownSidType, domainSid, pSid, ref cbSid);

      pSid = Marshal.AllocCoTaskMem(Convert.ToInt32(cbSid));
      if (NativeMethods.CreateWellKnownSid(wellKnownSidType, domainSid, pSid, ref cbSid))
      {
      NativeMethods.ConvertSidToStringSid(pSid, out sidString);
      }

      Marshal.FreeCoTaskMem(pSid);

      return sidString;
  }
```

## VB.Net Sample Code:
```cs
Private WinWorldSid As Integer = 1
    Private SECURITY_MAX_SID_SIZE As Integer = 68

    ' build a well-known SID for "Everyone"
    sidsize = SECURITY_MAX_SID_SIZE
    EveryoneSID = Marshal.AllocHGlobal(sidsize)
    If CreateWellKnownSid(WinWorldSid, IntPtr.Zero, EveryoneSID, sidsize) = False Then
        ret = Marshal.GetLastWin32Error()
        Throw New Win32Exception(ret)
    End If
```
