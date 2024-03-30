
## C# Signature: 
```cs
[DllImport("NetApi32.dll", CharSet=CharSet.Auto, SetLastError=true)] 
private static extern Int32 NetLocalGroupAddMembers( 
    string servername, //server name 
    string groupname, //group name 
    UInt32 level, //info level 
    ref LOCALGROUP_MEMBERS_INFO_3 buf, //Group info structure 
    UInt32 totalentries //number of entries 
    );
```

## VB Signature:
```cs
Declare Function NetLocalGroupAddMembers Lib "netapi32.dll" (TODO) As TODO
```

## Alternative Managed API:
```cs
private void AddDomainUserToLocalGroup( string userName,
                        string groupName, string domainName)
    {
        try
        {
        string computerName = SystemInformation.ComputerName;

        string localDirEntryString = "WinNT://" + computerName + ",computer";
        DirectoryEntry localDE = new DirectoryEntry(localDirEntryString);

        string domainDirEntryString = String.Format("WinNT://{0}", domainName);
        DirectoryEntry domainDE = new DirectoryEntry(domainDirEntryString);

        DirectoryEntry user = domainDE.Children.Find(userName, "user");
        DirectoryEntry group = localDE.Children.Find(groupName, "group");

        string invokeArg = user.Path.ToString();
        group.Invoke("Add", (object)invokeArg);
        }
        catch (DirectoryServicesCOMException e)
        {
        //trace the error
        }
        catch (TargetInvocationException tie)
        {
        //trace the error
        }
    }
```

## Sample Code:
```cs
using System;
    using System.Text;
    using System.Runtime.InteropServices;

    namespace ConsoleApplication3
    {

    class Program
    {
    [DllImport("advapi32.dll", CharSet = CharSet.Auto, SetLastError = true)]
    static extern bool LookupAccountSid(
        string SystemName,
        [MarshalAs(UnmanagedType.LPArray)] byte[] Sid,
        StringBuilder Name,
        ref uint NameCount,
        StringBuilder ReferencedDomainName,
        ref uint ReferencedDomainNameCount,
        out SID_NAME_USE SIDUse);

    [DllImport("netapi32.dll", SetLastError = true, CharSet = CharSet.Unicode)]
    extern static int NetLocalGroupAddMembers(string ServerName, string LocalGroupName,
        uint Level, ref LOCALGROUP_MEMBERS_INFO_3 MemberInfo, uint TotalEntries);

    //Error codes associated with 'NetLocalGroupAddMembers'
    //The local group specified by the groupname parameter does not exist. 
    private const int NERR_GroupNotFound = 2220;    
    //The user does not have access to the requested information. 
    private const int ERROR_ACCESS_DENIED = 5;
    // One or more of the members specified do not exist. Therefore, no new members were added. 
    private const int ERROR_NO_SUCH_MEMBER = 1387;
    // One or more of the members specified were already members of the local group. No new members were added. 
    private const int ERROR_MEMBER_IN_ALIAS = 1378;
    // One or more of the members cannot be added because their account type is invalid. No new members were added. 
    private const int ERROR_INVALID_MEMBER = 1388;

    struct LOCALGROUP_MEMBERS_INFO_3
    {
        [MarshalAs(UnmanagedType.LPWStr)]
        public string Domain;
    }

    [StructLayout(LayoutKind.Sequential)]
    private struct LOCALGROUP_MEMBERS_INFO_0
    {
        [MarshalAs(UnmanagedType.SysInt)]
        public IntPtr pSID;

    }

    enum SID_NAME_USE
    {
        SidTypeUser = 1,
        SidTypeGroup,
        SidTypeDomain,
        SidTypeAlias,
        SidTypeWellKnownGroup,
        SidTypeDeletedAccount,
        SidTypeInvalid,
        SidTypeUnknown,
        SidTypeComputer
    }

    private static class Win32ErrorCodes
    {
        internal const int NERR_Success         = 0x000;
        // Member alread in group.
        internal const int MemberInAlias        = 0x562;
    }

    static void Main(string[] args)
    {
        MakeUserAdmin(@"GEDEV\Engineer_1");
    }

    static bool MakeUserAdmin(string UserName)
    {
        bool bOk = false;

        StringBuilder sbName = new StringBuilder();
        uint uiName = (uint)sbName.Capacity;
        StringBuilder sbReferencedDomainName = new StringBuilder();
        uint uiReferencedDomainNameCount = (uint)sbReferencedDomainName.Capacity;
        SID_NAME_USE eUse;
        // Sid for BUILTIN\Administrators
        byte[] baSid = new byte[] { 1, 2, 0, 0, 0, 0, 0, 5, 32, 0, 0, 0, 32, 2 };

        if (!LookupAccountSid(null, baSid, sbName, ref uiName, sbReferencedDomainName, ref uiReferencedDomainNameCount, out eUse))
        return bOk;

        // prepare user name
        LOCALGROUP_MEMBERS_INFO_3 info;
        info.Domain = UserName;

        int iRetVal = 0;

        // add the user to the administrators group
        if ((iRetVal = NetLocalGroupAddMembers(null, sbName.ToString(), 3, ref info, 1)) != 0)
        return bOk;

        bOk = true;

        return bOk;
    }

    public static void AddMemberToLocalGroup(string groupName, SecurityIdentifier sid)
    {
        var sidBytes = new byte[sid.BinaryLength];
        sid.GetBinaryForm(sidBytes, 0);

        var info3 = new LOCALGROUP_MEMBERS_INFO_0
        {
            pSID = Marshal.AllocHGlobal(sidBytes.Length)
        };

        try
        {
            Marshal.Copy(sidBytes, 0, info3.pSID, sidBytes.Length);

            var result = NetLocalGroupAddMembers(null, groupName, 0, ref info3, 1);
            if (result == Win32ErrorCodes.NERR_Success || result == Win32ErrorCodes.MemberInAlias)
            {
                return;
            }

            throw new Win32Exception(result);
        }
        finally
        {
            Marshal.FreeHGlobal(info3.pSID);
        }
    }
    }
    }
```
