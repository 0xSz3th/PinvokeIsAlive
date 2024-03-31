
## C# Constants:
```cs
const int SECURITY_MANDATORY_UNTRUSTED_RID = (0x00000000);
    const int SECURITY_MANDATORY_LOW_RID = (0x00001000);
    const int SECURITY_MANDATORY_MEDIUM_RID = (0x00002000);
    const int SECURITY_MANDATORY_HIGH_RID = (0x00003000);
    const int SECURITY_MANDATORY_SYSTEM_RID = (0x00004000);
    const int SECURITY_MANDATORY_PROTECTED_PROCESS_RID = (0x00005000);
```

## VB Constants:
```cs
TODO
```

## Sample Code (C#):
```cs
try {
  UtIL.IntegrityLevel level = UtIL.GetIntegrityLevel();
}
catch (NotSupportedException) { // 2003 svr, XP, 2000, etc
  ...
}
```

## Sample Code (C#):
```cs
public enum IntegrityLevel {
  Low, Medium, High, System, None,
}
```

## Sample Code (C#):
```cs
using System;
using System.Runtime.InteropServices;
using System.Diagnostics;
using System.ComponentModel;

namespace ConsoleApplication1 {
    public class UtIL {
        [DllImport("advapi32.dll", SetLastError = true)]
        static extern IntPtr GetSidSubAuthority(IntPtr sid, UInt32 subAuthorityIndex);

        [DllImport("advapi32.dll", SetLastError = true)]
        static extern IntPtr GetSidSubAuthorityCount(IntPtr sid);

        // winnt.h, Windows SDK v6.1
        const int SECURITY_MANDATORY_UNTRUSTED_RID = (0x00000000);
        const int SECURITY_MANDATORY_LOW_RID = (0x00001000);
        const int SECURITY_MANDATORY_MEDIUM_RID = (0x00002000);
        const int SECURITY_MANDATORY_HIGH_RID = (0x00003000);
        const int SECURITY_MANDATORY_SYSTEM_RID = (0x00004000);
        const int SECURITY_MANDATORY_PROTECTED_PROCESS_RID = (0x00005000);

        [DllImport("advapi32.dll", SetLastError = true)]
        [return: MarshalAs(UnmanagedType.Bool)]
        static extern bool OpenProcessToken(
            IntPtr ProcessHandle,
            UInt32 DesiredAccess,
            out IntPtr TokenHandle
            );

        const UInt32 TOKEN_QUERY = 0x0008;

        [DllImport("advapi32.dll", SetLastError = true)]
        static extern bool GetTokenInformation(
            IntPtr TokenHandle,
            TOKEN_INFORMATION_CLASS TokenInformationClass,
            IntPtr TokenInformation,
            uint TokenInformationLength,
            out uint ReturnLength
            );

        enum TOKEN_INFORMATION_CLASS {
            TokenUser = 1, TokenGroups, TokenPrivileges, TokenOwner, TokenPrimaryGroup, TokenDefaultDacl, TokenSource, TokenType, TokenImpersonationLevel, TokenStatistics, TokenRestrictedSids, TokenSessionId, TokenGroupsAndPrivileges, TokenSessionReference, TokenSandBoxInert, TokenAuditPolicy, TokenOrigin, TokenElevationType, TokenLinkedToken, TokenElevation, TokenHasRestrictions, TokenAccessInformation, TokenVirtualizationAllowed, TokenVirtualizationEnabled,

            /// <summary>
            /// The buffer receives a TOKEN_MANDATORY_LABEL structure that specifies the token's integrity level. 
            /// </summary>
            TokenIntegrityLevel,

            TokenUIAccess, TokenMandatoryPolicy, TokenLogonSid, MaxTokenInfoClass
        }

        // http://d.hatena.ne.jp/espresso3389/20100413/1271152244
        // http://msdn.microsoft.com/en-us/library/bb625966.aspx

        const int ERROR_INVALID_PARAMETER = 87;

        [DllImport("kernel32.dll", SetLastError = true)]
        static extern bool CloseHandle(IntPtr hHandle);

        public enum IntegrityLevel {
            Low, Medium, High, System, None,
        }

        public static IntegrityLevel GetIntegrityLevel() {
            IntPtr pId = (Process.GetCurrentProcess().Handle);

            IntPtr hToken = IntPtr.Zero;
            if (OpenProcessToken(pId, TOKEN_QUERY, out hToken)) {
                try {
                    IntPtr pb = Marshal.AllocCoTaskMem(1000);
                    try {
                        uint cb = 1000;
                        if (GetTokenInformation(hToken, TOKEN_INFORMATION_CLASS.TokenIntegrityLevel, pb, cb, out cb)) {
                            IntPtr pSid = Marshal.ReadIntPtr(pb);

                            int dwIntegrityLevel = Marshal.ReadInt32(GetSidSubAuthority(pSid, (Marshal.ReadByte(GetSidSubAuthorityCount(pSid)) - 1U)));

                            if (dwIntegrityLevel == SECURITY_MANDATORY_LOW_RID) {
                                return IntegrityLevel.Low;
                            }
                            else if (dwIntegrityLevel >= SECURITY_MANDATORY_MEDIUM_RID && dwIntegrityLevel < SECURITY_MANDATORY_HIGH_RID) {
                                // Medium Integrity
                                return IntegrityLevel.Medium;
                            }
                            else if (dwIntegrityLevel >= SECURITY_MANDATORY_HIGH_RID) {
                                // High Integrity
                                return IntegrityLevel.High;
                            }
                            else if (dwIntegrityLevel >= SECURITY_MANDATORY_SYSTEM_RID) {
                                // System Integrity
                                return IntegrityLevel.System;
                            }
                            return IntegrityLevel.None;
                        }
                        else {
                            int errno = Marshal.GetLastWin32Error();
                            if (errno == ERROR_INVALID_PARAMETER) {
                                throw new NotSupportedException();
                            }
                            throw new Win32Exception(errno);
                        }
                    }
                    finally {
                        Marshal.FreeCoTaskMem(pb);
                    }
                }
                finally {
                    CloseHandle(hToken);
                }
            }
            {
                int errno = Marshal.GetLastWin32Error();
                throw new Win32Exception(errno);
            }
        }

        static void Main(string[] args) {
            try {
                // Output candidates:

                // Not supported!
                // Medium
                // High

                Console.WriteLine(UtIL.GetIntegrityLevel());
            }
            catch (Exception) {
                Console.WriteLine("Not supported!");
            }
        }
    }
}
```
