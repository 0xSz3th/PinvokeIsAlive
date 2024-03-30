
## Sample Code:
```cs
public int GetRemoteAuditPolicy(ref string[,] Policies)
    {
        Policies = new string[9, 2] { { "System", "" }, { "Logon", "" }, { "Object Access", "" }, { "Privilige Use", "" }, { "Detailed Tracking", "" }, { "Policy Change", "" }, { "Account Management", "" }, { "Directory Service Access", "" }, { "Account Logon", "" } };

        //Everything from here until the "Good Stuff", was copied from this site
        byte[] Sid = null;
        uint cbSid = 0;
        StringBuilder referencedDomainName = new StringBuilder();
        uint cchReferencedDomainName = (uint)referencedDomainName.Capacity;
        SID_NAME_USE sidUse;

        int err = 0;
        if (!LookupAccountName(this.ResourceName, this.UserName, Sid, ref cbSid, referencedDomainName, ref cchReferencedDomainName, out sidUse))
        {
        err = Marshal.GetLastWin32Error();
        if (err == ERROR_INSUFFICIENT_BUFFER || err == ERROR_INVALID_FLAGS)
        {
            Sid = new byte[cbSid];
            referencedDomainName.EnsureCapacity((int)cchReferencedDomainName);
            err = 0;
            if (!LookupAccountName(this.ResourceName, this.UserName, Sid, ref cbSid, referencedDomainName, ref cchReferencedDomainName, out sidUse))
            err = Marshal.GetLastWin32Error();
            //throw error here
            //return custom error constant
        }
        }

        LSA_UNICODE_STRING aSystemName = new LSA_UNICODE_STRING();

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

        IntPtr aPolicyHandle = IntPtr.Zero;
        uint infoclass = (uint)POLICY_INFORMATION_CLASS.PolicyAuditEventsInformation;
        IntPtr bufptr = IntPtr.Zero;

        LSA_OBJECT_ATTRIBUTES aObjectAttributes = new LSA_OBJECT_ATTRIBUTES();
        aObjectAttributes.Length = 0;
        aObjectAttributes.RootDirectory = IntPtr.Zero;
        aObjectAttributes.Attributes = 0;
        aObjectAttributes.SecurityDescriptor = IntPtr.Zero;
        aObjectAttributes.SecurityQualityOfService = IntPtr.Zero;

        aSystemName.SetTo(this.ResourceName);

        uint aOpenPolicyResult = LsaOpenPolicy(ref aSystemName, ref aObjectAttributes, aAccess, out aPolicyHandle);

        //Here's the "Good Stuff" folks
        //This example gets Audit Policy information
        uint retval = LsaQueryInformationPolicy(aPolicyHandle, infoclass, out bufptr);
        //do what you want with the retval, this is a pretty lazy example

        _POLICY_AUDIT_EVENTS_INFO pevents;

        //Marshal the pointer to structure; pretty standard stuff
        pevents = (_POLICY_AUDIT_EVENTS_INFO)Marshal.PtrToStructure(bufptr, typeof(_POLICY_AUDIT_EVENTS_INFO));

        //Microsoft states that this could be an arbitrary number of elements because they may expand upon this in later Windows versions
        int[] policy_values = new int[pevents.MaximumAuditEventCount];

        //pevents.MaximumAuditEventCount gives you the number of elements, take this number of elements and Marshall copy the array
        Marshal.Copy(pevents.EventAuditingOptions, policy_values, 0, pevents.MaximumAuditEventCount);

        //Only take the lowest array count
        int max_policies = Policies.GetLength(0);
        max_policies = max_policies > pevents.MaximumAuditEventCount ? pevents.MaximumAuditEventCount : max_policies;

        //Grade 10 programming class
        for (int x = 0; x < max_policies; x++)
        {
        switch (policy_values[x])
        {
            case 0:
            Policies[x, 1] = "None";
            break;
            case 1:
            Policies[x, 1] = "Success";
            break;
            case 2:
            Policies[x, 1] = "Failure";
            break;
            case 3:
            Policies[x, 1] = "Success/Failure";
            break;
        }
        }
        return 0;
    }
```

## Sample Code:
```cs
enum POLICY_INFORMATION_CLASS
     {
         PolicyAuditLogInformation = 1,
         PolicyAuditEventsInformation,
         PolicyPrimaryDomainInformation,
         PolicyPdAccountInformation,
         PolicyAccountDomainInformation,
         PolicyLsaServerRoleInformation,
         PolicyReplicaSourceInformation,
         PolicyDefaultQuotaInformation,
         PolicyModificationInformation,
         PolicyAuditFullSetInformation,
         PolicyAuditFullQueryInformation,
         PolicyDnsDomainInformation 
    }

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

## Sample Code:
```cs
public struct _POLICY_AUDIT_EVENTS_INFO
     {
         public bool AuditingMode;
         public IntPtr EventAuditingOptions;
         public Int32 MaximumAuditEventCount;
     }

    Microsoft also has an enumeration for the different policies; but like I said above, they strongly caution you to not fix the number of elements in the array because that can and probably will change.  Use my array at the top of the function for now.

    Happy coding!  http://digitalboundary.net
```
