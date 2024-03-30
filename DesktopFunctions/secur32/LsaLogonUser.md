
## C# Signature:
```cs
[DllImport("secur32.dll", SetLastError=false)]
public static extern WinStatusCodes LsaLogonUser(
                    [In] IntPtr LsaHandle,
                    [In] ref LSA_STRING OriginName,
                    [In] SecurityLogonType LogonType,
                    [In] UInt32 AuthenticationPackage,
                    [In] IntPtr AuthenticationInformation,
                    [In] UInt32 AuthenticationInformationLength,
                    [In] /*PTOKEN_GROUPS*/ IntPtr LocalGroups,
                    [In] ref TOKEN_SOURCE SourceContext,
                    [Out] /*PVOID*/ out IntPtr ProfileBuffer,
                    [Out] out UInt32 ProfileBufferLength,
                    [Out] out Int64 LogonId,
                    [Out] out IntPtr Token,
                    [Out] out QUOTA_LIMITS Quotas,
                    [Out] out WinStatusCodes SubStatus
                    );
```

## VB Signature:
```cs
Declare Function LsaLogonUser Lib "secur32.dll" (TODO) As TODO
```

## Sample Code:
```cs
using System;
using System.Runtime.InteropServices;

namespace CCSecurityUtilities
{
    /// <remarks>
    /// This sample uses S4U security, which requires Windows Server 2003 and a W2003 domain controller
    /// </remarks>
    public sealed class CCWinLogonUtilities
    {
        private CCWinLogonUtilities()
        {
        }
```

## Sample Code:
```cs
#region "Win32 stuff"
        private class Win32
        {
            internal class OSCalls
            {
                public enum WinStatusCodes : uint
                {
                    STATUS_SUCCESS = 0
                }

                public enum WinErrors : uint
                {
                    NO_ERROR = 0,
                }
                public enum WinLogonType
                {
                    LOGON32_LOGON_INTERACTIVE       =2,
                    LOGON32_LOGON_NETWORK       =3,
                    LOGON32_LOGON_BATCH         =4,
                    LOGON32_LOGON_SERVICE       =5,
                    LOGON32_LOGON_UNLOCK        =7,
                    LOGON32_LOGON_NETWORK_CLEARTEXT =8,
                    LOGON32_LOGON_NEW_CREDENTIALS   =9
                }

                // SECURITY_LOGON_TYPE
                public enum SecurityLogonType
                {
                    Interactive = 2,    // Interactively logged on (locally or remotely)
                    Network,        // Accessing system via network
                    Batch,          // Started via a batch queue
                    Service,        // Service started by service controller
                    Proxy,          // Proxy logon
                    Unlock,         // Unlock workstation
                    NetworkCleartext,   // Network logon with cleartext credentials
                    NewCredentials,     // Clone caller, new default credentials
                    RemoteInteractive,  // Remote, yet interactive. Terminal server
                    CachedInteractive,  // Try cached credentials without hitting the net.
                    CachedRemoteInteractive, // Same as RemoteInteractive, this is used internally for auditing purpose
                    CachedUnlock    // Cached Unlock workstation
                }

                [StructLayout(LayoutKind.Sequential)]
                    public struct LSA_UNICODE_STRING 
                {
                    public UInt16 Length;
                    public UInt16 MaximumLength;
                    public IntPtr Buffer;
                }

                [StructLayout(LayoutKind.Sequential)]
                    public struct TOKEN_SOURCE
                {
                    public TOKEN_SOURCE(string name)
                    {
                        SourceName = new byte[8];
                        System.Text.Encoding.GetEncoding(1252).GetBytes(name,0,name.Length,SourceName,0);
                        if (!AllocateLocallyUniqueId(out SourceIdentifier))
                            throw new System.ComponentModel.Win32Exception();
                    }

                    [MarshalAs(UnmanagedType.ByValArray,SizeConst=8)] public byte[] SourceName;
                    public UInt64 SourceIdentifier;
                }

                [StructLayout(LayoutKind.Sequential)]
                    public struct QUOTA_LIMITS 
                {
                    UInt32 PagedPoolLimit;
                    UInt32 NonPagedPoolLimit;
                    UInt32 MinimumWorkingSetSize;
                    UInt32 MaximumWorkingSetSize;  
                    UInt32 PagefileLimit;  
                    Int64 TimeLimit;
                }

                [StructLayout(LayoutKind.Sequential)]
                    public struct LSA_STRING 
                {
                    public UInt16 Length;
                    public UInt16 MaximumLength;
                    public /*PCHAR*/ IntPtr Buffer;
                }

                public class LsaStringWrapper : IDisposable
                {
                    public LSA_STRING _string;

                    public LsaStringWrapper(string value)
                    {
                        _string = new LSA_STRING();
                        _string.Length = (ushort)value.Length;
                        _string.MaximumLength = (ushort)value.Length;
                        _string.Buffer = Marshal.StringToHGlobalAnsi(value);
                    }

                    ~LsaStringWrapper()
                    {
                        Dispose(false);
                    }

                    private void Dispose(bool disposing)
                    {
                        if (_string.Buffer != IntPtr.Zero)
                        {
                            Marshal.FreeHGlobal(_string.Buffer);
                            _string.Buffer = IntPtr.Zero;
                        }
                        if (disposing)
                            GC.SuppressFinalize(this);
                    }

                    #region IDisposable Members

                    public void Dispose()
                    {
                        Dispose(true);
                    }

                    #endregion
                }
```

## Sample Code:
```cs
public class KerbS4ULogon : IDisposable
                {
                    [StructLayout(LayoutKind.Sequential)]
                        public struct KERB_S4U_LOGON 
                    {
                        public Int32 MessageType;    // Should be 12
                        public Int32 Flags; // Reserved, should be 0
                        public LSA_UNICODE_STRING ClientUpn;   // REQUIRED: UPN for client
                        public LSA_UNICODE_STRING ClientRealm; // Optional: Client Realm, if known
                    }

                    public KerbS4ULogon(string clientUpn) : this(clientUpn,null)
                    {
                    }

                    public KerbS4ULogon(string clientUpn,string clientRealm)
                    {
                        int clientUpnLen = (clientUpn == null) ? 0 : clientUpn.Length;
                        int clientRealmLen = (clientRealm == null) ? 0 : clientRealm.Length;
                        _bufferLength = Marshal.SizeOf(typeof(KERB_S4U_LOGON)) + 2 * (clientUpnLen + clientRealmLen);
                        _bufferContent = Marshal.AllocHGlobal(_bufferLength);
                        if (_bufferContent == IntPtr.Zero)
                            throw new OutOfMemoryException("Could not allocate memory for KerbS4ULogon structure");
                        try
                        {
                            KERB_S4U_LOGON baseStructure = new KERB_S4U_LOGON();
                            baseStructure.MessageType = 12;    // KerbS4ULogon
                            baseStructure.Flags = 0;
                            baseStructure.ClientUpn.Length = (UInt16)(2*clientUpnLen);
                            baseStructure.ClientUpn.MaximumLength = (UInt16)(2*clientUpnLen);
                            IntPtr curPtr = new IntPtr(_bufferContent.ToInt32()+Marshal.SizeOf(typeof(KERB_S4U_LOGON)));
                            if (clientUpnLen > 0)
                            {
                                baseStructure.ClientUpn.Buffer = curPtr;
                                Marshal.Copy(clientUpn.ToCharArray(),0,curPtr,clientUpnLen);
                                curPtr = new IntPtr(curPtr.ToInt32()+clientUpnLen*2);
                            }
                            else
                                baseStructure.ClientUpn.Buffer = IntPtr.Zero;
                            baseStructure.ClientRealm.Length = (UInt16)(2*clientRealmLen);
                            baseStructure.ClientRealm.MaximumLength = (UInt16)(2*clientRealmLen);
                            if (clientRealmLen > 0)
                            {
                                baseStructure.ClientRealm.Buffer = curPtr;
                                Marshal.Copy(clientRealm.ToCharArray(),0,curPtr,clientRealmLen);
                            }
                            else
                                baseStructure.ClientRealm.Buffer = IntPtr.Zero;
                            Marshal.StructureToPtr(baseStructure,_bufferContent,false);
                        }
                        catch
                        {
                            Dispose(true);
                            throw;
                        }
                    }

                    private IntPtr _bufferContent;
                    private int _bufferLength;

                    public IntPtr Ptr
                    {
                        get {return _bufferContent;}
                    }

                    public int Length
                    {
                        get {return _bufferLength;}
                    }

                    private void Dispose(bool disposing)
                    {
                        if (_bufferContent != IntPtr.Zero)
                        {
                            Marshal.FreeHGlobal(_bufferContent);
                            _bufferContent = IntPtr.Zero;
                        }
                        if (disposing)
                            GC.SuppressFinalize(this);
                    }

                    ~KerbS4ULogon()
                    {
                        Dispose(false);
                    }

                    #region IDisposable Members

                    public void Dispose()
                    {
                        Dispose(true);
                    }

                    #endregion
                }

                [DllImport("advapi32.dll", CharSet=CharSet.Auto, SetLastError=false)]
                public static extern WinErrors LsaNtStatusToWinError(WinStatusCodes status);

                [DllImport("advapi32.dll", CharSet=CharSet.Auto, SetLastError=true)]
                public static extern bool AllocateLocallyUniqueId([Out] out UInt64 Luid);

                [DllImport("kernel32.dll", CharSet=CharSet.Auto, SetLastError=true)]
                public static extern int CloseHandle(IntPtr hObject);

                [DllImport("secur32.dll", SetLastError=false)]
                public static extern WinStatusCodes LsaLogonUser(
                    [In] IntPtr LsaHandle,
                    [In] ref LSA_STRING OriginName,
                    [In] SecurityLogonType LogonType,
                    [In] UInt32 AuthenticationPackage,
                    [In] IntPtr AuthenticationInformation,
                    [In] UInt32 AuthenticationInformationLength,
                    [In] /*PTOKEN_GROUPS*/ IntPtr LocalGroups,
                    [In] ref TOKEN_SOURCE SourceContext,
                    [Out] /*PVOID*/ out IntPtr ProfileBuffer,
                    [Out] out UInt32 ProfileBufferLength,
                    [Out] out Int64 LogonId,
                    [Out] out IntPtr Token,
                    [Out] out QUOTA_LIMITS Quotas,
                    [Out] out WinStatusCodes SubStatus
                    );

                [DllImport("secur32.dll", SetLastError=false)]
                public static extern WinStatusCodes LsaFreeReturnBuffer(
                    [In] IntPtr buffer);

                [DllImport("secur32.dll", SetLastError=false)]
                public static extern WinStatusCodes LsaConnectUntrusted([Out] out IntPtr LsaHandle);

                [DllImport("secur32.dll", SetLastError=false)]
                public static extern WinStatusCodes LsaDeregisterLogonProcess([In] IntPtr LsaHandle);

                [DllImport("secur32.dll", SetLastError=false)]
                public static extern WinStatusCodes LsaLookupAuthenticationPackage([In] IntPtr LsaHandle,[In] ref LSA_STRING PackageName,[Out] out UInt32 AuthenticationPackage);

            }

            public sealed class HandleSecurityToken
                : IDisposable
            {
                private IntPtr m_hToken = IntPtr.Zero;

                // using S4U logon
                public HandleSecurityToken(string UserName,
                    string Domain,
                    OSCalls.WinLogonType LogonType
                    )
                {
                    using (OSCalls.KerbS4ULogon authPackage = new OSCalls.KerbS4ULogon(UserName,Domain))
                    {
                        IntPtr lsaHandle;
                        OSCalls.WinStatusCodes status = OSCalls.LsaConnectUntrusted(out lsaHandle);
                        if (status != OSCalls.WinStatusCodes.STATUS_SUCCESS)
                            throw new System.ComponentModel.Win32Exception((int)OSCalls.LsaNtStatusToWinError(status));
                        try
                        {
                            UInt32 kerberosPackageId;
                            using (OSCalls.LsaStringWrapper kerberosPackageName = new OSCalls.LsaStringWrapper("Kerberos"))
                            {
                                status = OSCalls.LsaLookupAuthenticationPackage(lsaHandle,ref kerberosPackageName._string,out kerberosPackageId);
                                if (status != OSCalls.WinStatusCodes.STATUS_SUCCESS)
                                    throw new System.ComponentModel.Win32Exception((int)OSCalls.LsaNtStatusToWinError(status));
                            }
                            OSCalls.LsaStringWrapper originName = null;
                            try
                            {
                                originName = new OSCalls.LsaStringWrapper("CCSecurityUtilities");
                                OSCalls.TOKEN_SOURCE sourceContext = new OSCalls.TOKEN_SOURCE("CCSecUt");
                                System.IntPtr profileBuffer = IntPtr.Zero;
                                UInt32 profileBufferLength = 0;
                                Int64 logonId;
                                OSCalls.WinStatusCodes subStatus;
                                OSCalls.QUOTA_LIMITS quotas;
                                status = OSCalls.LsaLogonUser(
                                    lsaHandle,
                                    ref originName._string,
                                    (OSCalls.SecurityLogonType)LogonType,
                                    kerberosPackageId,
                                    authPackage.Ptr,
                                    (uint)authPackage.Length,
                                    IntPtr.Zero,
                                    ref sourceContext,
                                    out profileBuffer,
                                    out profileBufferLength,
                                    out logonId,
                                    out m_hToken,
                                    out quotas,
                                    out subStatus);
                                if (status != OSCalls.WinStatusCodes.STATUS_SUCCESS)
                                    throw new System.ComponentModel.Win32Exception((int)OSCalls.LsaNtStatusToWinError(status));
                                if (profileBuffer != IntPtr.Zero)
                                    OSCalls.LsaFreeReturnBuffer(profileBuffer);
                            }
                            finally
                            {
                                if (originName != null)
                                    originName.Dispose();
                            }
                        }
                        finally
                        {
                            OSCalls.LsaDeregisterLogonProcess(lsaHandle);
                        }
                    }
                }

                ~HandleSecurityToken()
                {
                    Dispose(false);
                }

                public void Dispose() 
                {
                    Dispose(true);
                }

                private void Dispose(bool disposing )
                {
                    lock(this)
                    {
                        if (!m_hToken.Equals(IntPtr.Zero))
                        {
                            OSCalls.CloseHandle(m_hToken);
                            m_hToken = IntPtr.Zero;
                        }
                        if (disposing)
                            GC.SuppressFinalize(this);
                    }
                }

                public System.Security.Principal.WindowsIdentity BuildIdentity()
                {
                    System.Security.Principal.WindowsIdentity retVal = new System.Security.Principal.WindowsIdentity(m_hToken);
                    GC.KeepAlive(this);
                    return retVal;
                }
            }

        }

        #endregion
```

## Sample Code:
```cs
/// <summary>
        /// The Windows Logon Types.
        /// </summary>
        public enum WinLogonType
        {
            /// <summary>
            /// Interactive logon
            /// </summary>
            LOGON32_LOGON_INTERACTIVE       = Win32.OSCalls.WinLogonType.LOGON32_LOGON_INTERACTIVE,
            /// <summary>
            /// Network logon
            /// </summary>
            LOGON32_LOGON_NETWORK       = Win32.OSCalls.WinLogonType.LOGON32_LOGON_NETWORK,
            /// <summary>
            /// Batch logon
            /// </summary>
            LOGON32_LOGON_BATCH         = Win32.OSCalls.WinLogonType.LOGON32_LOGON_BATCH,
            /// <summary>
            /// Logon as a service
            /// </summary>
            LOGON32_LOGON_SERVICE       = Win32.OSCalls.WinLogonType.LOGON32_LOGON_SERVICE,
            /// <summary>
            /// Unlock logon
            /// </summary>
            LOGON32_LOGON_UNLOCK        = Win32.OSCalls.WinLogonType.LOGON32_LOGON_UNLOCK,
            /// <summary>
            /// Preserve password logon
            /// </summary>
            LOGON32_LOGON_NETWORK_CLEARTEXT = Win32.OSCalls.WinLogonType.LOGON32_LOGON_NETWORK_CLEARTEXT,
            /// <summary>
            /// Current token for local access, credentials for network access
            /// </summary>
            LOGON32_LOGON_NEW_CREDENTIALS   = Win32.OSCalls.WinLogonType.LOGON32_LOGON_NEW_CREDENTIALS
        }

        /// <summary>
        /// Logs in a credential for server apps. No need to provide password.
        /// </summary>
        /// <param name="credential">The credential to log in. Password is ignored.</param>
        /// <param name="logonType">The type of logon to use</param>
        /// <remarks>
        /// Requires Windows Server 2003 domain account running in Win2003 native domain mode
        /// </remarks>
        /// <returns>Returns a <c>System.Security.Principal.WindowsIdentity</c> object</returns>
        /// Raises an exception with error information if the user cannot log in
        public static System.Security.Principal.WindowsIdentity CreateIdentityS4U(System.Net.NetworkCredential credential, WinLogonType logonType)
        {
            using (Win32.HandleSecurityToken handleToken =
                       new Win32.HandleSecurityToken(credential.UserName,credential.Domain,(Win32.OSCalls.WinLogonType)logonType))
                return handleToken.BuildIdentity();
        }

    }
}
```
