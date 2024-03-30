
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError=true, PreserveSig=true)]
static extern uint LsaOpenPolicy(
   ref LSA_UNICODE_STRING SystemName,
   ref LSA_OBJECT_ATTRIBUTES ObjectAttributes,
   uint DesiredAccess,
   out IntPtr PolicyHandle
);
```

## VB Signature:
```cs
Declare Unicode Function LsaOpenPolicy Lib "advapi32.dll" ( _
    ByRef SystemName As LSA_UNICODE_STRING, _
    ByRef ObjectAttributes As LSA_OBJECT_ATTRIBUTES, _
    ByVal DesiredAccess As Int32, _
    ByRef PolicyHandle As IntPtr) As Int32
```

## Sample Code:
```cs
public static uint SetRight( string inAccountName, string inPrivilegeName )
{
    uint aWinErrorCode = 0; //contains the last error

    //pointer an size for the SID
    IntPtr aSid = IntPtr.Zero;
    int aSidSize = 0;

    //StringBuilder and size for the domain name
    StringBuilder aDomainName = new StringBuilder();
    int aNameSize = 0;
    //account-type variable for lookup
    int aAccountType = 0;

    //get required buffer size
    LookupAccountName( String.Empty, inAccountName, aSid, ref aSidSize, aDomainName, ref aNameSize, ref aAccountType );

    //allocate buffers
    aDomainName = new StringBuilder( aNameSize );
    aSid = Marshal.AllocHGlobal( aSidSize );

    //lookup the SID for the account
    bool aResult = LookupAccountName( String.Empty, inAccountName, aSid, ref aSidSize, aDomainName, ref aNameSize, ref aAccountType );

    if ( aResult )
    {
        //initialize an empty unicode-string
        LSA_UNICODE_STRING aSystemName = new LSA_UNICODE_STRING();
        //combine all policies
        uint aAccess = (uint)(
            LSA_AccessPolicy.POLICY_AUDIT_LOG_ADMIN |
            LSA_AccessPolicy.POLICY_CREATE_ACCOUNT |
            LSA_AccessPolicy.POLICY_CREATE_PRIVILEGE |
            LSA_AccessPolicy.POLICY_CREATE_SECRET |
            LSA_AccessPolicy.POLICY_GET_PRIVATE_INFORMATION |
            LSA_AccessPolicy.POLICY_LOOKUP_NAMES |
            LSA_AccessPolicy.POLICY_NOTIFICATION | 
            LSA_AccessPolicy.POLICY_SERVER_ADMIN |
            LSA_AccessPolicy.POLICY_SET_AUDIT_REQUIREMENTS |
            LSA_AccessPolicy.POLICY_SET_DEFAULT_QUOTA_LIMITS |
            LSA_AccessPolicy.POLICY_TRUST_ADMIN |
            LSA_AccessPolicy.POLICY_VIEW_AUDIT_INFORMATION |
            LSA_AccessPolicy.POLICY_VIEW_LOCAL_INFORMATION
            );
        //initialize a pointer for the policy handle
        IntPtr aPolicyHandle = IntPtr.Zero;

        //these attributes are not used, but LsaOpenPolicy wants them to exists
        LSA_OBJECT_ATTRIBUTES aObjectAttributes = new LSA_OBJECT_ATTRIBUTES();
        aObjectAttributes.Length = 0;
        aObjectAttributes.RootDirectory = IntPtr.Zero;
        aObjectAttributes.Attributes = 0;
        aObjectAttributes.SecurityDescriptor = IntPtr.Zero;
        aObjectAttributes.SecurityQualityOfService = IntPtr.Zero;            

        //get a policy handle
        uint aOpenPolicyResult = LsaOpenPolicy(ref aSystemName, ref aObjectAttributes, aAccess, out aPolicyHandle);
        aWinErrorCode = LsaNtStatusToWinError( aOpenPolicyResult );

        if( aWinErrorCode == Win32Constants.STATUS_SUCCESS )
        {
            //Now that we have the SID an the policy,
            //we can add rights to the account.
            //initialize an unicode-string for the privilege name
            LSA_UNICODE_STRING[] aUserRightsLSAString = new LSA_UNICODE_STRING[1];
            aUserRightsLSAString[0] = new LSA_UNICODE_STRING();
            aUserRightsLSAString[0].Buffer = Marshal.StringToHGlobalUni( inPrivilegeName );
            aUserRightsLSAString[0].Length = ( UInt16 )( inPrivilegeName.Length * UnicodeEncoding.CharSize );
            aUserRightsLSAString[0].MaximumLength = ( UInt16 )( ( inPrivilegeName.Length + 1 ) * UnicodeEncoding.CharSize );

            //add the right to the account
            uint aLSAResult = LsaAddAccountRights( aPolicyHandle, aSid, aUserRightsLSAString, 1 );
            aWinErrorCode = LsaNtStatusToWinError( aLSAResult );

            LsaClose( aPolicyHandle );
        }
        FreeSid( aSid );

    }
    else
    {
        aWinErrorCode = (uint)GetLastError();
    }

    return aWinErrorCode;
}
```

## Alternate Sample Code:
```cs
// This was started from the sample code above (which I originally found on code project).

    [StructLayout(LayoutKind.Sequential)]
    internal struct LSA_UNICODE_STRING
    {
        public UInt16 Length;
        public UInt16 MaximumLength;
        public IntPtr Buffer;

        public void SetTo(string str)
        {
            Buffer = Marshal.StringToHGlobalUni(str);
            Length = (UInt16)(str.Length * UnicodeEncoding.CharSize);
            MaximumLength = (UInt16)(Length + UnicodeEncoding.CharSize);
            //Console.WriteLine("SetTo: {2} ({3}) Length: {0} Max: {1}", Length, MaximumLength, str, str.Length);
        }

        public override string ToString()
        {
            string str = Marshal.PtrToStringUni(Buffer, Length/UnicodeEncoding.CharSize);
            //Console.WriteLine("ToString: {2} ({3}) Length: {0} Max: {1}", Length, MaximumLength, str, str.Length);
            return str;
        }

        public void Clean()
        {
            //Console.WriteLine("Clean Length: {0} Max: {1}", Length, MaximumLength);
            if (Buffer != IntPtr.Zero)
                Marshal.FreeHGlobal(Buffer);
            Buffer = IntPtr.Zero;
            Length = 0;
            MaximumLength = 0;
        }
    };

    public class LSAStringMarshaler : ICustomMarshaler
    {
        Hashtable myAllocated = new Hashtable();

        private static LSAStringMarshaler marshaler = new LSAStringMarshaler();
        public static ICustomMarshaler GetInstance(string cookie)
        {
            return marshaler;
        }

        public object MarshalNativeToManaged(System.IntPtr pNativeData)
        {
            if (pNativeData != IntPtr.Zero)
            {
                LSA_UNICODE_STRING lus = (LSA_UNICODE_STRING) Marshal.PtrToStructure(pNativeData, typeof(LSA_UNICODE_STRING));
                return lus.ToString();
            }
            return null;
        }

        private static readonly int nativeSize = IntPtr.Size + sizeof(UInt16) + sizeof(UInt16);

        public System.IntPtr MarshalManagedToNative(object ManagedObj)
        {
            LSA_UNICODE_STRING lus = new LSA_UNICODE_STRING();
            IntPtr memory = Marshal.AllocHGlobal(nativeSize);
            myAllocated[memory] = memory;
            //Console.WriteLine("MarshalManagedToNative");
            lus.SetTo((string)ManagedObj);
            Marshal.StructureToPtr(lus, memory, true);
            return memory;
        }

        public void CleanUpManagedData(object ManagedObj)
        {
            //Console.WriteLine("CCC Cleanup Managed Data");            
        }

        public int GetNativeDataSize()
        {
            return nativeSize;
        }

        public void CleanUpNativeData(System.IntPtr pNativeData)
        {            
            //Console.WriteLine("CCC Cleanup Native Data");            

            if (myAllocated.ContainsKey(pNativeData))
            {
                myAllocated.Remove(pNativeData);
                LSA_UNICODE_STRING lus = (LSA_UNICODE_STRING) Marshal.PtrToStructure(pNativeData, typeof(LSA_UNICODE_STRING));
                lus.Clean();
                Marshal.FreeHGlobal(pNativeData);
            }
        }
    }

    public class LSAPolicy : IDisposable
    {
        private IntPtr policy;

        [Flags]
        public enum LSA_AccessPolicy : long
        {
            POLICY_VIEW_LOCAL_INFORMATION = 0x00000001L,
            POLICY_VIEW_AUDIT_INFORMATION = 0x00000002L,
            POLICY_GET_PRIVATE_INFORMATION = 0x00000004L,
            POLICY_TRUST_ADMIN = 0x00000008L,
            POLICY_CREATE_ACCOUNT = 0x00000010L,
            POLICY_CREATE_SECRET = 0x00000020L,
            POLICY_CREATE_PRIVILEGE = 0x00000040L,
            POLICY_SET_DEFAULT_QUOTA_LIMITS = 0x00000080L,
            POLICY_SET_AUDIT_REQUIREMENTS = 0x00000100L,
            POLICY_AUDIT_LOG_ADMIN = 0x00000200L,
            POLICY_SERVER_ADMIN = 0x00000400L,
            POLICY_LOOKUP_NAMES = 0x00000800L,
            POLICY_NOTIFICATION = 0x00001000L
        }
```

## Alternate Sample Code:
```cs
public LSAPolicy() : this (
            LSA_AccessPolicy.POLICY_AUDIT_LOG_ADMIN |
            LSA_AccessPolicy.POLICY_CREATE_ACCOUNT |
            LSA_AccessPolicy.POLICY_CREATE_PRIVILEGE |
            LSA_AccessPolicy.POLICY_CREATE_SECRET |
            LSA_AccessPolicy.POLICY_GET_PRIVATE_INFORMATION |
            LSA_AccessPolicy.POLICY_LOOKUP_NAMES |
            LSA_AccessPolicy.POLICY_NOTIFICATION |
            LSA_AccessPolicy.POLICY_SERVER_ADMIN |
            LSA_AccessPolicy.POLICY_SET_AUDIT_REQUIREMENTS |
            LSA_AccessPolicy.POLICY_SET_DEFAULT_QUOTA_LIMITS |
            LSA_AccessPolicy.POLICY_TRUST_ADMIN |
            LSA_AccessPolicy.POLICY_VIEW_AUDIT_INFORMATION |
            LSA_AccessPolicy.POLICY_VIEW_LOCAL_INFORMATION
            )
        {}

        public LSAPolicy(LSA_AccessPolicy access)
        {
            //initialize an empty unicode-string
            string systemName = null;

            //these attributes are not used, but LsaOpenPolicy wants them to exist
            // (MSDN: "the structure members are not used, initalize them to NULL or zero")
            LSA_OBJECT_ATTRIBUTES ObjectAttributes = new LSA_OBJECT_ATTRIBUTES();
            ObjectAttributes.Length = 0;
            ObjectAttributes.RootDirectory = IntPtr.Zero;
            ObjectAttributes.Attributes = 0;
            ObjectAttributes.SecurityDescriptor = IntPtr.Zero;
            ObjectAttributes.SecurityQualityOfService = IntPtr.Zero;

            //get a policy handle
            UInt32 resultPolicy = LsaOpenPolicy(ref systemName, ref ObjectAttributes, (int)access, out policy);
            UInt32 winErrorCode = LsaNtStatusToWinError(resultPolicy);

            if (winErrorCode != 0)
            {
                throw new Win32Exception(winErrorCode, "OpenPolicy failed: ");
            }

        }

        ~LSAPolicy()
        {
            Dispose(false);
        }

        public void Dispose()
        {
            Dispose(true);
            GC.SuppressFinalize(this);
        }

        public void Dispose(bool disposing)
        {
            if (policy != IntPtr.Zero)
            {
                LsaClose(policy);
                policy = IntPtr.Zero;
            }
        }

        public string RetrievePrivateData(string key)
        {
            string result = null;
            UInt32 ntstatus = LsaRetrievePrivateData(policy, key, ref result);
            UInt32 winErrorCode = LsaNtStatusToWinError(ntstatus);
            if (winErrorCode != 0)
            {
                throw new Exception("RetreivePrivateData failed: " + winErrorCode);
            }
            return result;
        }

        public void StorePrivateData(string key, string value)
        {
            UInt32 ntstatus = LsaStorePrivateData(policy, key, value);
            UInt32 winErrorCode = LsaNtStatusToWinError(ntstatus);
            if (winErrorCode != 0)
            {
                throw new Exception("RetreivePrivateData failed: " + winErrorCode);
            }
        }

        [DllImport("advapi32.dll")]
        private static extern UInt32 LsaRetrievePrivateData(
            IntPtr policyHandle,
            [MarshalAs(UnmanagedType.CustomMarshaler,MarshalTypeRef=typeof(LSAStringMarshaler))] string KeyName,
            [MarshalAs(UnmanagedType.CustomMarshaler,MarshalTypeRef=typeof(LSAStringMarshaler))] ref string PrivateData
        );

        [DllImport("advapi32.dll")]
        private static extern uint LsaStorePrivateData(
        IntPtr policyHandle,
            [MarshalAs(UnmanagedType.CustomMarshaler, MarshalTypeRef = typeof(LSAStringMarshaler))]  string KeyName,
            [MarshalAs(UnmanagedType.CustomMarshaler, MarshalTypeRef = typeof(LSAStringMarshaler))]  string PrivateData
        );

        [DllImport("advapi32.dll")]
        private static extern long LsaClose(IntPtr ObjectHandle);

        [StructLayout(LayoutKind.Sequential)]
        private struct LSA_OBJECT_ATTRIBUTES
        {
            public int Length;
            public IntPtr RootDirectory;
            public LSA_UNICODE_STRING ObjectName;
            public UInt32 Attributes;
            public IntPtr SecurityDescriptor;
            public IntPtr SecurityQualityOfService;
        }

        [DllImport("advapi32.dll", PreserveSig=true)]
        private static extern UInt32 LsaOpenPolicy(
            [MarshalAs(UnmanagedType.CustomMarshaler,MarshalTypeRef=typeof(LSAStringMarshaler))] ref string SystemName,
            ref LSA_OBJECT_ATTRIBUTES ObjectAttributes,
            Int32 DesiredAccess,
            out IntPtr PolicyHandle
        );

        [DllImport("advapi32.dll")]
        private static extern UInt32 LsaNtStatusToWinError(UInt32 status);

    }
```

## VB.Net Sample Code:
```cs
' Check to see if the Deny permission already exists
    Public Function CheckTS(ByVal PC As String) As Boolean
    Dim ret, Access, sidsize, count, i As Integer
    Dim SystemName, DenyTSRights As LSA_UNICODE_STRING
    Dim ObjectAttr As LSA_OBJECT_ATTRIBUTES
    Dim Policy, EveryoneSID, EnumBuf, ptr As IntPtr
    Dim LsaInfo As LSA_ENUMERATION_INFORMATION
    Dim ans As Boolean

    ' build a well-known SID for "Everyone"
    sidsize = SECURITY_MAX_SID_SIZE
    EveryoneSID = Marshal.AllocHGlobal(sidsize)
    If CreateWellKnownSid(WinWorldSid, IntPtr.Zero, EveryoneSID, sidsize) = False Then
        ret = Marshal.GetLastWin32Error()
        Throw New Win32Exception(ret)
    End If

    ' setup the parameters for the LsaOpenPolicy API
    ObjectAttr.Length = Marshal.SizeOf(ObjectAttr)
    SystemName.Length = PC.Length * UnicodeEncoding.CharSize
    SystemName.MaximumLength = (PC.Length + 1) * UnicodeEncoding.CharSize
    SystemName.Buffer = Marshal.StringToHGlobalUni(PC)
    Access = POLICY_ALL_ACCESS

    ' open a policy handle on the remote PC
    ret = LsaOpenPolicy(SystemName, ObjectAttr, Access, Policy)
    If ret <> 0 Then
        Throw New Win32Exception(LsaNtStatusToWinError(ret))
    End If

    ' clean up
    Marshal.FreeHGlobal(SystemName.Buffer)

    ' Setup the input parameters for the LsaEnumerateAccountsWithUserRight API
    DenyTSRights.Length = SE_DENY_REMOTE_INTERACTIVE_LOGON_NAME.Length * UnicodeEncoding.CharSize
    DenyTSRights.MaximumLength = (SE_DENY_REMOTE_INTERACTIVE_LOGON_NAME.Length + 1) * UnicodeEncoding.CharSize
    DenyTSRights.Buffer = Marshal.StringToHGlobalUni(SE_DENY_REMOTE_INTERACTIVE_LOGON_NAME)

    ' do it!
    ret = LsaEnumerateAccountsWithUserRight(Policy, DenyTSRights, EnumBuf, count)
    If ret <> 0 Then
        Marshal.FreeHGlobal(DenyTSRights.Buffer)
        LsaClose(Policy)
        ' if there are no matching entries
        If ret = STATUS_NO_MORE_ENTRIES Then
        Return False
        End If
        Throw New Win32Exception(LsaNtStatusToWinError(ret))
    End If

    ' check to see if the Everyone SID is currently in the list
    ans = False
    For i = 0 To count - 1
        ptr = New IntPtr(EnumBuf.ToInt32 + (i * Marshal.SizeOf(LsaInfo)))
        LsaInfo = CType(Marshal.PtrToStructure(ptr, GetType(LSA_ENUMERATION_INFORMATION)), LSA_ENUMERATION_INFORMATION)
        If EqualSid(LsaInfo.Sid, EveryoneSID) Then
        ans = True
        Exit For
        End If
    Next

    ' clean up
    LsaFreeMemory(EnumBuf)
    Marshal.FreeHGlobal(DenyTSRights.Buffer)
    LsaClose(Policy)

    Return ans
    End Function
```
